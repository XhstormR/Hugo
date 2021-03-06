---
author: XhstormR
categories:
- Assembly
date: 2020-04-24T10:26:27+08:00
title: Assembly language
---

<!--more-->

Updated on 2020-04-24

>

## 指令
* `MOV AL, 10H`
* 指令 = `操作码 操作数`
* 操作数 = `目的操作数(R/W), 源操作数(RO)`

### 数据传送指令
* 通用传送指令
  * 基本传送指令：`MOV dst, src`
  * 栈指令：`PUSH src`、`POP dst`
    * 以字为单位操作
  * 交换指令：`XCHG dst, src`
    * 以字或字节为单位操作
    * 寄存器之间、寄存器和存储器之间
* 累加器传送指令
  * 输入指令：`IN`
  * 输出指令：`OUT`
* 地址传送指令
  * LEA：将源操作数的偏移地址传送到目的操作数
  * LDS：将源操作数的 4 个相继字节的数据分别发送给目的操作数和 DS 寄存器
    * `LDS DI, [BX]`
    * DI <- DS + BX
    * DS <- DS + BX + 2
  * LES
* 标志传送指令
  * LAHF
    * AH <- PSW 的低 8 位
  * SAHF
    * AH -> PSW 的低 8 位
  * PUSHF
  * POPF

### 算术运算指令
* 加法指令
  * ADD：无进位加法指令
    * 指令影响标志位
      * 有符号运算超出范围，则 OF 为 1
      * 无符号运算超出范围，则 CF 为 1
  * ADC：带进位加法指令
  * INC：自增 1 指令
* 减法指令
  * SUB：无进位减法指令
  * SBB：带进位减法指令
  * DEC：自减 1 指令
  * NEG：求补指令
    * 转为补码（把操作数按位取反后末位加一）
  * CMP：比较指令
    * 不保留结果，只影响标志位
    * 根据 Z 标志位，判断两数是否相等
    * 根据 C 标志位，判断两个无符号数的大小
    * 根据 S、O 标志位，判断两个有符号数的大小
* 乘法指令
  * MUL：无符号乘法
  * IMUL：有符号乘法
* 除法指令
  * DIV：无符号除法
  * IDIV：有符号除法

### 位运算指令
* OR：或指令
* NOT：非指令
* AND：与指令
* XOR：异或指令
* TEST：测试指令
  * 规则等同于与指令
  * 不保留结果，只影响标志位

### 移位指令
* SAL：算术左移
* SAR：算术右移
  * 最高位不变
* SHL：逻辑左移
* SHR：逻辑右移
* ROL：无进位循环左移
  * 左边移出的位补到右边，并送入 CF
* ROR：无进位循环右移
  * 右边移出的位补到左边，并送入 CF
* RCL：带进位循环左移
  * 原 CF 到右边，左边送入 CF
* RCR：带进位循环右移
  * 原 CF 到左边，右边送入 CF

## 操作数存放位置
* 存放于指令中（立即数）
  * `MOV AL, 10H` 中的 `10H`
* 存放于寄存器中（寄存器操作数）
  * `INC CX` 中的 `CX`
* 存放于存储器中（存储器操作数）
  * `MOV AX, [2500H]` 中的 `[2500H]`

## 寻址方式分类
* 地址寄存器
  * 基址寄存器：BX、BP
  * 变址寄存器：SI、DI
  * 默认操作数存放于 DS 段寄存器：BX、SI、DI。
  * 默认操作数存放于 SS 段寄存器：BP。
* 立即数寻址方式
  * `MOV AL, 10H`
* 寄存器寻址方式
  * `INC CX`
* 存储器寻址方式
  * 直接寻址方式
    * `MOV AX, [2500H]`
    * `MOV AX, ES:[1064H]`（段超越：操作数不在默认的 DS 段中）
  * 寄存器间接寻址方式
    * 操作数的偏移地址存放于寄存器当中。
    * `MOV AX, [SI]`
    * `MOV [BX], AL`
    * `MOV AX, SS:[SI]`（段超越：操作数不在默认段中）
  * 寄存器相对寻址方式
    * 寄存器间接寻址方式 + 指令中给定的偏移量。
    * `MOV CL, [BX+1064H]`
  * 基址加变址寻址方式
    * 段寄存器 + 基址寄存器 + 变址寄存器。
    * `MOV AH, [BP][SI]`
      * `[BP][SI]` = SS + BP + SI = 40000H + 2000H + 1200H
  * 相对基址加变址寻址方式
    * 基址加变址寻址方式 + 指令中给定的偏移量。
    * `MOV [BX+DI+1234H], AH`
      * `[BX+DI+1234H]` = DS + BX + DI + 1234H = 20000H + 0200H + 0010H + 1234H
