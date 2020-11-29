---
title: Insertion Sort List（連結リストの挿入ソート）
date: '2020-11-25'
template: 'post'
draft: false
slug: 'leetcode-linked-list'
category: 'Algorithm'
tags:
  - 'Algorithm'
  - 'LeetCode'

description: 'ここ最近、AtCoderの過去問に取り組んでいるのですが、気まぐれでLeetCodeを覗いてみました。そこで「単連結リスト」に出会ったので、少しだけメモします。'
# socialImage: '/media/image-2.jpg'
---

アルゴリズムには大学一年生からずっと頭を悩まされている気がします。。。
実験中に眠気に襲われ、LeetCode の[147. Insertion Sort List](https://leetcode.com/problems/insertion-sort-list/)を眠気覚ましに解きました。<br>
ある日の C 言語の授業で躓いた思い出がある「連結リスト（Linked list）」なる言葉が出てきたので、用語の方をメモ程度にまとめておきます。詳細は問題の解説に任せます。

## 問題の概要

単連結リストに対して挿入ソートを行うアルゴリズムを実装せよ。

## 用語たち

### 単方向連結リスト

連結リスト：データ構造の１つで、一つの単位（ノード）はある値とあるノードへの参照を持つ。配列と比較される。
単方向：参照の方向が片方のみであること。参照がお互いにある場合は双方向。

Python の list は（動的）配列です（たぶん）。

### 挿入ソート

既にソート済みの配列にある値を挿入して再びソート済みの配列にしていく、並び替えのアルゴリズムの１つ。配列だと時間計算量が` O(N^2)`かかる。

## 本題 ： 単方向連結リストの挿入ソート

### ポイント

配列のソートの動きを真似する感じ？

1. 配列の挿入ソートのように、ソート済みの連結リストを用意する
2. ソート済み配列の先頭のノードから挿入したいノードの値を比較していく
3. 2.を実装するために、「今から挿入するノード」の参照を用意する

### 実装

```python
class Solution:
    def insertionSortList(self, head: ListNode) -> ListNode:
        # 3 つのポインタを考える
        # curr: 今から挿入しようとしているノード
        # prev: currと比較するノード（初期値は空のdummyノード）
        # curr.next: curr の次のノード
        dummy = ListNode()
        curr = head
        while curr:
            prev = dummy

            # prev を curr と比較していき、curr の挿入位置を見つける
            while prev.next:
                if prev.next.val > curr.val:break
                prev = prev.next

            next = curr.next
            curr.next = prev.next
            prev.next = curr
            curr = next  # 次のノードを挿入する準備

        return dummy.next
```

提出結果は[こちら](https://leetcode.com/submissions/detail/423965338/)

また、忘れるだろうけど、年一くらいで思い出していけば OK！
