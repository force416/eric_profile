---
title: java實作linkedlist
toc: true
comments: true
date: 2016-07-28 23:38:23
description:
tags:
    - LinkedList
categories:
    - java
---
### 前言
* 去面試時被問到如何實作LinkedList，結果答不出來，回家google練習
* 本篇只有Java程式碼
### 實作

```java
public class LinkedList<T> {

	public static void main(String[] args) {
		LinkedList<String> testList = new LinkedList<String>();
		testList.add("eric");
		testList.add("is");
		testList.add("a");
		testList.add("pig");
		System.out.println(testList.get(2));
		System.out.println(testList.size());
		testList.remove(2);
		System.out.println(testList.get(2));
		System.out.println(testList.size());
		testList.add("shih", 1);
		System.out.println(testList.get(1));
		System.out.println(testList.size());
	}

	private Node<T> head;

	private int count;

	public T get(int index) {
		if (index >= count || index < 0) {
			return null;
		}
		if (head != null) {
			if (index == 0) {
				return head.getValue();
			}
			Node<T> resultNode = head;
			for (int i=0; i< index; i++) {
				resultNode = resultNode.getNextNode();
			}
			return resultNode.getValue();
		}
		return null;
	}

	public boolean add(T object) {
		if (head == null) {
			head = new Node<T>(object);
		} else {
			Node<T> currentNode = head;
			while (currentNode.getNextNode() != null) {
				currentNode = currentNode.getNextNode();
			}
			currentNode.setNextNode(new Node<T>(object));
		}
		count++;
		return true;
	}

	public boolean add(T object, int index) {
		//add first
		if (index == 0 && head == null) {
			head = new Node<T>(object);
		}else if (index == 0 && head != null) {
			Node<T> tmpNode = new Node<T>(object);
			tmpNode.setNextNode(head);
			head = tmpNode;
		}

		if (head != null) {
			Node<T> currentNode = head;
			Node<T> tmpNode = new Node<T>(object);
			index--;
			for (int i = 0; i< index; i++) {
				if (currentNode.getNextNode() != null) {
					currentNode = currentNode.getNextNode();
				}
			}
			tmpNode.setNextNode(currentNode.getNextNode());
			currentNode.setNextNode(tmpNode);
		}
		count++;
		return true;
	}

	public boolean remove(int index) {
		if (index == 0 && head != null && head.getNextNode() == null) {
			head = null;
			count--;
			return true;
		}
		if (head != null) {
			Node<T> currentNode = head;
			index--;
			for (int i = 0; i< index; i++) {
				if (currentNode.getNextNode() != null) {
					currentNode = currentNode.getNextNode();
				}
			}
			currentNode.setNextNode(currentNode.getNextNode().getNextNode());
		}
		count--;
		return true;
	}

	public int size() {
		return this.count;
	}

	/**
	 * LinkedList 使用節點模型
	 * inner class
	 */
	private class Node<T> {

		/** 目前節點的值*/
		private T value;
		/** 下個節點*/
		private Node<T> nextNode;

		public Node(T object) {
			this.value = object;
		}

		public T getValue() {
			return value;
		}
		public void setValue(T value) {
			this.value = value;
		}
		public Node<T> getNextNode() {
			return nextNode;
		}
		public void setNextNode(Node<T> nextNode) {
			this.nextNode = nextNode;
		}
	}
}
```

### LinkedList 概念
* 參考 (https://www.cs.cmu.edu/~adamchik/15-121/lectures/Linked%20Lists/linked%20lists.html)
* 參考 (https://crunchify.com/how-to-implement-a-linkedlist-class-from-scratch-in-java/)
