GFW Research
================

:Date: 02/03 2018

.. contents::


西厢计划
---------

`西厢计划` 提供一组工具，使得用户在一次设置之后，能够以普通程序直连目标网络，而避免GFW的大部分影响。
其命名是为了向中国古典文学史上翻墙的先驱者张某致敬。

西厢计划现在已经达到 `alpha` 可用状态，在初步的测试中可以让用户以普通浏览器无障碍地直连 `Youtube`。


西厢计划第一季
~~~~~~~~~~~~~~~~~~~

:GoogleCode: `p/scholarzhang <https://code.google.com/archive/p/scholarzhang>`_
:Github: `codegooglecom/scholarzhang <https://github.com/codegooglecom/scholarzhang>`_


解决问题:

*   `TCP` 连接重置
*   `DNS` 劫持（污染）

方法:

*   TCP连接混淆

    在每次连接中，通过对GFW的入侵检测系统进行注入，混淆连接，使得GFW无法正确解析连接和检测关键词，
    从而在有关键词的情况下也避免连接重置。(更新，2011年7月测试，客户端的TCP连接混淆已经不可用)

*   反DNS劫持

    通过匹配GFW伪包的指纹并将其过滤，让用户以普通的客户端也能获得正确的解析结果。
    （用户需要设置DNS为没有被污染的DNS，例如178.79.131.110 等）

原理:

    规避入侵检测的注入方法 是指发出特制报文，使得这些报文对对方没有效果，
    但是让IDS错误地分析协议，从而让IDS错误地认为连接被提前终止了。

    由于GFW的TCP栈非常简陋，因此我们可以直接利用GFW的TCP栈的特性，
    对任何遵守RFC的目标主机都采取特定特殊措施，让GFW无法正确解析TCP连接，
    从而避免关键词监测。


局限:

    西厢计划的连接混淆功能对于基于 `IP地址` 的封锁和其他无状态的封锁不能生效，
    因为它需要通过注入攻击改变GFW的连接状态，如果封锁与连接状态无关便无法进行连接混淆。
    另外，连接混淆的实现假设连接双方遵守RFC。有一些目标主机或者防火墙不遵守RFC，
    可能导致正常不含关键词的连接被对方终止或者忽略。


西厢计划第二季
~~~~~~~~~~~~~~~

:Code: `gamehacker/west-chamber-season-2 <https://github.com/gamehacker/west-chamber-season-2>`_

解决问题:

*   单向 `IP` 封锁
*   `HTTP URL` 关键词过滤

方法:

*   阻止路由器发来的 `ttl exceeded` 消息
*   将发出数据的 `TTL` 设置为 `5` ，不会到达 `GFW`


原理:

    利用GFW的单向IP封锁特性，将 发出 的数据包通过国外的第三方服务器中转，
    而收到的数据包 穿过GFW直接到达客户端 。

    当用HTTP方式观看在线视频或下载大文件时，对中转服务器仅耗费 极小的流量 。

    同时，由于GFW只能捕捉到单向的流量， 无法建立TCP状态机 无法获取请求URL，
    关键词过滤也就失效了。

.. NOTE::
    
    《西厢计划第二季》为独立的新项目，与原西厢计划没有关联，只是借用了一下品牌。
    西厢计划第二季和西厢计划都是 `tech demo` ，发布出来仅作研究用途。


西厢计划第三季
~~~~~~~~~~~~~~~

:Code: `liruqi/west-chamber-season-3 <https://github.com/liruqi/west-chamber-season-3>`_

.. NOTE::

    基本没有提出什么新思路。


INTANG
---------

*   `seclab-ucr/INTANG <https://github.com/seclab-ucr/INTANG>`_ , INTANG is research project for circumventing the "TCP reset attack" from the Great Firewall of China (GFW) by disrupting/desynchronizing the TCP Control Block (TCB) on the censorship devices.
