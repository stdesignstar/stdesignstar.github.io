---
title: A* Algorithm
author: stdesignstar
date: 2022-01-22 12:00:00 +09:00
categories: [PathFind]
tags: [PathFind]
math: true
mermaid: true
---

## 개요

A* 알고리즘의 정리.

## 내용  
```cs
public class AStarPathFinder
{
    public class Node
    {
        public Point2 CellPoint { get; }
        public int F => G + H;
        public int G { get; private set; } // start -> current
        public int H { get; private set; } // current -> end
        public Node Parent;

        public Node(int x, int y)
        {
            CellPoint = new Point2(x, y);
        }

        public void Execute(Node parent, Node end)
        {
            Parent = parent;

            G = CalcG(parent, this);

            var diffX = Mathf.Abs(parent.CellPoint.X - end.CellPoint.X);
            var diffY = Mathf.Abs(parent.CellPoint.Y - end.CellPoint.Y);

            H = (diffX + diffY) * 10;
        }

        public static int CalcG(Node parent, Node current)
        {
            var diffX = Mathf.Abs(parent.CellPoint.X - current.CellPoint.X);
            var diffY = Mathf.Abs(parent.CellPoint.Y - current.CellPoint.Y);

            return diffX == diffY ? diffX * 14 : (diffX + diffY) * 10 + parent.G;
        }
    }

    public Point2 Size => new Point2(_nodes.GetLength(0), _nodes.GetLength(1));

    private Node[,] _nodes;
    private int[,] _obstacles;

    private readonly List<Node> _openList = new List<Node>();
    private readonly List<Node> _closeList = new List<Node>();

    public void Setup(int x, int y)
    {
        _nodes = new Node[x, y];

        for (var i = 0; i < x; ++i)
        {
            for (var j = 0; j < y; ++j)
            {
                _nodes[i, j] = new Node(i, j);
            }
        }

        _obstacles = new int[x, y];
    }

    public void SetupObstacles(int[,] obstacles)
    {
        if (_obstacles.GetLength(0) != obstacles.GetLength(0) ||
            _obstacles.GetLength(1) != obstacles.GetLength(1))
        {
            return;
        }

        for (var i = 0; i < _obstacles.GetLength(0); ++i)
        {
            for (var j = 0; j < _obstacles.GetLength(1); ++j)
            {
                _obstacles[i, j] = obstacles[i, j];
            }
        }
    }

    public void SetupObstacles(int x, int y, int value)
    {
        if (x >= _obstacles.GetLength(0) || y >= _obstacles.GetLength(1))
        {
            return;
        }

        _obstacles[x, y] = value;
    }

    public void ClearFindDatas()
    {
        _openList.Clear();
        _closeList.Clear();

        for (var i = 0; i < _nodes.GetLength(0); ++i)
        {
            for (var j = 0; j < _nodes.GetLength(1); ++j)
            {
                _nodes[i, j].Parent = null;
            }
        }
    }

    public void ClearObstacles()
    {
        for (var i = 0; i < _obstacles.GetLength(0); ++i)
        {
            for (var j = 0; j < _obstacles.GetLength(1); ++j)
            {
                _obstacles[i, j]= 0;
            }
        }
    }

    public IReadOnlyList<Node> Find(Point2 startCellPoint, Point2 endCellPoint)
    {
        var start = _nodes[startCellPoint.X, startCellPoint.Y];
        var end = _nodes[endCellPoint.X, endCellPoint.Y];

        return Find(start, end);
    }

    private IReadOnlyList<Node> Find(Node start, Node end)
    {
        if (start == null || end == null)
        {
            return null;
        }

        ClearFindDatas();

        _openList.Add(start);

        Node current = null;
        do
        {
            if (_openList.IsEmpty())
            {
                break;
            }

            current = _openList.OrderBy(e => e.F).First();
            _openList.Remove(current);
            _closeList.Add(current);
            if (current == end)
            {
                break;
            }
            for (var i = 0; i < _nodes.GetLength(0); ++i)
            {
                for (var j = 0; j < _nodes.GetLength(1); ++j)
                {
                    // 8 way
                    //bool isNear = (Math.Abs(current.X - _nodes[i, j].X) <= 1)
                    //         && (Math.Abs(current.Y - _nodes[i, j].Y) <= 1);
                    // 4 way
                    var isNear = (Math.Abs(current.CellPoint.X - _nodes[i, j].CellPoint.X) <= 1)
                             && (Math.Abs(current.CellPoint.Y - _nodes[i, j].CellPoint.Y) <= 1)
                             && (current.CellPoint.Y == _nodes[i, j].CellPoint.Y || current.CellPoint.X == _nodes[i, j].CellPoint.X);

                    var isObstacle = _obstacles[i, j] > 0;

                    if (isObstacle
                     || _closeList.Contains(_nodes[i, j])
                     || isNear == false)
                    {
                        continue;
                    }

                    if (_openList.Contains(_nodes[i, j]) == false)
                    {
                        _openList.Add(_nodes[i, j]);
                        _nodes[i, j].Execute(current, end);
                    }
                    else
                    {
                        if (Node.CalcG(current, _nodes[i, j]) < _nodes[i, j].G)
                        {
                            _nodes[i, j].Execute(current, end);
                        }
                    }
                }
            }
        } while (current != null);

        if (current != end)
        {
            // can not found root
            return null;
        }

        var path = new List<Node>();
        do
        {
            path.Add(current);
            current = current.Parent;
        }
        while (current != null);

        path.Reverse();

        return path;
    }
}

public struct Point2
{
    public int X;
    public int Y;

    public Point2(int x, int y)
    {
        X = x;
        Y = y;
    }

    public bool Equals(int x, int y)
    {
        return X == x && Y == y;
    }

    public override bool Equals(object obj)
    {
        if (!(obj is Point2 point2))
        {
            return false;
        }

        return this.Equals(point2.X, point2.Y);
    }

    public override int GetHashCode()
    {
        return base.GetHashCode();
    }

    public static Point2 operator +(Point2 a, Point2 b)
    {
        return new Point2(a.X + b.X, a.Y + b.Y);
    }

    public static bool operator ==(Point2 a, Point2 b)
    {
        return a.X == b.X && a.Y == b.Y;
    }

    public static bool operator !=(Point2 a, Point2 b)
    {
        return !(a == b);
    }
}
```
## Reference  
https://ko.wikipedia.org/wiki/A*_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98  