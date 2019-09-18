---
layout:     post   				    # 使用的布局（不需要改）
title:      Build Multi-threaded Dictionary Server 				# 标题 
subtitle:                #副标题
date:       2019-8-21 				# 时间
author:     Lingxuan Kong 						# 作者
header-img: img/computer-coffee.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags: 							#标签
    - Java
    - JavaSwing
---

## 1. Introduction

This is assignment 1 of Distributed Systems (COMP90015), we are going to use a client-server architecture, design and implement a multi-threaded server that allows concurrent clients to search the meaning(s) of a word, add a new word, and remove an existing word. 

This assignment will focus on two technologies:

- Sockets
- Threads



## 2. Architecture

1. The system will follow a client-server architecture in which multiple clients can connect to a (single) multi-threaded server and perform operations concurrently.
2. The multi-threaded server may implement a **thread-per-request**, **thread-per-connection**, or **worker pool** architecture.



## 3. Interaction

All communication will take place via sockets. These sockets can be either **TCP(Connection-Oriented)** or **UDP(Connectionless)**. Thus, in this project, I am goind to use **TCP** for its reliable connection.

The data format will be **JSON**.



## 4. Function

### 4.1 Query the meaning(s) of a given word

The client should implement a function that is used to query the dictionary with the following minimum input and output. 

- **Input**: Target word to query.
- **Output:** The meaning of target word.
- **Error:** The target word is not in the dictionary or an error occur. 