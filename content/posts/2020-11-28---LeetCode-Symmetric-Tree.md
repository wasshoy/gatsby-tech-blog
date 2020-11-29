---
title: Symmetric Tree（二分木の対称性）
date: '2020-11-28'
template: 'post'
draft: false
slug: 'leetcode-symmetric-tree'
category: 'Algorithm'
tags:
  - 'Algorithm'
  - 'LeetCode'

description: '夜中に起きて眠れなかったので、LeetCodeを覗いてみました。今回は「二分木の対称性」に関する問題を解いたので、メモしておきます。'
---

夜中に起きてしまったので、なんとか眠ろうと頭の中で BFS の実装を復習していましたが、眠れませんでした。
そこで、「LeetCode BFS」でなんとなく検索したらこの問題[](https://leetcode.com/problems/symmetric-tree/)がが出てきたので、取り組んでみました。

## 問題の概要

二分木が与えられるので、左右対称かを判定せよ（再帰的に / 繰り返しで解いて）。

## 用語たち

### 木

閉路を持たない連結無向グラフ。データ構造。
ある頂点を一番上と見ると、それにぶら下がるように他の頂点を見ることができる。
これを根付き木という（木って基本これのことかと思ってた）。

### 二分木

各節点（木の頂点のこと）の子が、最大で 2 つである木。

## ポイント

ある木が左右対称であるには、**左右の部分木（根の子を根とする木）が左右対称である**必要がある。

また、2 つの木が左右対称であるには、

1. 根が同じ値
2. 各木の右部分木はもう一方の木の左部分木と**左右対称（再帰部分）**

である必要がある。

## 実装

ポイントの処理を分けて書くと分かりやすい。
再帰的な書き方はまあまあ苦手。先に言葉にした方が分かりやすいかも？？

```python
class Solution:
    # 2つの木が左右対称であるかどうか
    def isMirror(self, lnode: TreeNode, rnode: TreeNode) -> bool:
        if lnode == None and rnode == None: return True
        if lnode == None or rnode == None: return False
        return (lnode.val == rnode.val  # 根が同じ値
            and self.isMirror(lnode.left, rnode.right)  # 左と右の部分木が左右対称
            and self.isMirror(lnode.right, rnode.left)  # 右と左の部分木が左右対称
        )

    def isSymmetric(self, root: TreeNode) -> bool:
        if root == None:
            return True
        return self.isMirror(root.left, root.right)
```
