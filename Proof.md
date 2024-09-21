​        我将证明在现有的知识库中，**不可能通过$SLD$算法下利用消解原理得到单子句**，并且我采用了对单子句的产生过程进行回溯和排查的方式。这里提供一个更详细的推导过程，帮助你建立这种证明。

### 证明方法

1. **知识库的构成**：
   你的知识库包含以下公式（以 $ V(x) $ 表示顶点，$E(x,y) $ 表示边，$R(x) ,  G(x) , B(x) $分别表示顶点 $x$  染色：

   - 对每个节点，有以下公式：

     $V(x) \Rightarrow R(x) \lor G(x) \lor B(x)$即每个顶点必须染成红、绿、蓝中的一种颜色。

     $V(x)$

   - 对每条边 , y)，如果两个顶点 $x $ 和 $ y $ 的颜色相同，那么就会产生矛盾（即不能同色）：
     $E(x, y) \land R(x) \land R(y) \Rightarrow UnCol$
     
     $E(x,y)$
     
   - 将知识库中的所有内容化为合取范式便于消解
     $$
     1.  (R(a) \lor G(a) \lor B(a) \lor \neg V(a)) \\
     2.  (R(b) \lor G(b) \lor B(b) \lor \neg V(b)) \\
     3.  (R(c) \lor G(c) \lor B(c) \lor \neg V(c)) \\
     4.  (R(d) \lor G(d) \lor B(d) \lor \neg V(d)) \\
     
     - 顶点 a 和 b 之间的边:\\
       1.  (\neg E(a, b) \lor \neg R(a) \lor \neg R(b) \lor UnCol) \\
       2.  (\neg E(a, b) \lor \neg G(a) \lor \neg G(b) \lor UnCol) \\
       3.  (\neg E(a, b) \lor \neg B(a) \lor \neg B(b) \lor UnCol) \\
     
     - 顶点 a 和 c 之间的边:\\
       1.  (\neg E(a, c) \lor \neg R(a) \lor \neg R(c) \lor UnCol) \\
       2.  (\neg E(a, c) \lor \neg G(a) \lor \neg G(c) \lor UnCol) \\
       3.  (\neg E(a, c) \lor \neg B(a) \lor \neg B(c) \lor UnCol) \\
     $$

     $$
     - 顶点 a 和 d 之间的边:\\
       1.  (\neg E(a, d) \lor \neg R(a) \lor \neg R(d) \lor UnCol) \\
       2.  (\neg E(a, d) \lor \neg G(a) \lor \neg G(d) \lor UnCol) \\
       3.  (\neg E(a, d) \lor \neg B(a) \lor \neg B(d) \lor UnCol) \\
     
     - 顶点 b 和 c 之间的边:\\
       1.  (\neg E(b, c) \lor \neg R(b) \lor \neg R(c) \lor UnCol) \\
       2.  (\neg E(b, c) \lor \neg G(b) \lor \neg G(c) \lor UnCol) \\
       3.  (\neg E(b, c) \lor \neg B(b) \lor \neg B(c) \lor UnCol) \\
     
     $$
     
     $$
     - 顶点 b 和 d 之间的边:\\
       1.  (\neg E(b, d) \lor \neg R(b) \lor \neg R(d) \lor UnCol) \\
       2.  (\neg E(b, d) \lor \neg G(b) \lor \neg G(d) \lor UnCol) \\
       3.  (\neg E(b, d) \lor \neg B(b) \lor \neg B(d) \lor UnCol) \\
     
     - 顶点 c 和 d 之间的边:\\
       1.  (\neg E(c, d) \lor \neg R(c) \lor \neg R(d) \lor UnCol) \\
       2.  (\neg E(c, d) \lor \neg G(c) \lor \neg G(d) \lor UnCol) \\
       3.  (\neg E(c, d) \lor \neg B(c) \lor \neg B(d) \lor UnCol) \\
       - 顶点与连边信息
     V(a) ,V(b),V(c) ,V(d) \\
     E(a, b),E(a, c),E(a, d),E(c, b),E(d, b),E(c, d)\\
     $$
     
     
   
2. **消解原理的回溯分析**：
   消解原理的目标是通过现有的子句推导出更简单的子句，最终尝试推导出单子句甚至空子句。证明中需要说明**无法通过现有子句消解出单子句**，即：当前知识库中没有一种消解序列能够在不引入新子句的情况下推导出单子句。

   

3. **回溯和排查**：
            回溯方法是通过分析消解过程中可能推导出单子句的路径，逐步排查每个可能性，最后得出结论：每一条推导路径都需要引入新的子句，而这些新子句是现有知识库中不存在的。

   **引理1：每次消解得到的子句最多比上一步参与消解的最长的子句的长度减少一个**

   >​        假设我们有两个子句 $C_1$ 和 $C_2$，其中 $C_1$ 和 $C_2$ 含有一个互为否定的文字 $p$ 和 $\neg p$。我们需要证明，进行一次消解操作后，新生成的子句的长度最多减少一个。
   >
   >设定：
   >
   >- $C_1$ 的长度为 $|C_1|$。
   >- $C_2$ 的长度为 $|C_2|$。
   >- $C_1$ 包含文字 $p$。
   >- $C_2$ 包含文字 $\neg p$。
   >
   >消解操作：
   >通过消解，我们得到一个新子句 $C$，该子句包含 $C_1$ 和 $C_2$ 的所有文字，除了 $p$ 和 $\neg p$ 之外。
   >
   >证明：
   >
   >新子句的构造： 新子句 $C$ 是从 $C_1$ 和 $C_2$ 中删除文字 $p$ 和 $\neg p$ 后，合并剩余文字得到的。具体来说，
   >
   >$C=(C_1−\{p\})∪(C_2−\{¬p\})C=(C_1−\{p\})∪(C_2−\{¬p\})$
   >
   >长度的计算：
   >
   >- $|C_1 - {p}|$ 是去掉 $p$ 后的 $C_1$ 的长度，即 $|C_1| - 1$（如果 $p$ 存在于 $C_1$ 中）。
   >- $|C_2 - {\neg p}|$ 是去掉 $\neg p$ 后的 $C_2$ 的长度，即 $|C_2| - 1$（如果 $\neg p$ 存在于 $C_2$ 中）。
   >
   >合并后的长度： 新子句的长度 $|C|$ 是去掉 $p$ 和 $\neg p$ 后的子句的并集长度。
   >
   >$∣C∣=∣(C_1−\{p\})∪(C_2−\{¬p\})∣\\≥max\{∣C_1−\{p\}|,|C_2−\{¬p\}|\}=max\{∣C_1|,|C_2|\}-1$
   >
   >所以，新子句 $C$ 的长度比上一步参与消解的最长的子句的长度最多减少一个。
   >
   >引理证毕！

   **引理2：对于一个由两个否定字母（谓词）的析取范式，任何字句都无法通过消解推导出一个正字句（即，不含有否定符号的单子句）**

   >考虑一个由两个否定的字母构成的析取范式（Disjunctive Normal Form, DNF）：
   >
   >设该范式为 $\neg P \vee \neg Q$，表示两个否定字母的析取（"或"关系）。
   >
   >**我们要证明：** 不存在一个子句可以通过与 $\neg P \vee \neg Q$ 进行消解，得到一个正的单子句（如 $P$ 或 $Q$）。
   >
   >**消解规则**
   >
   >消解法则允许在两个子句中找到互补的文字（一个子句中是肯定的，另一个子句中是否定的），然后去掉这些互补文字，得到一个新子句。例如：
   >
   >- 对于 $P \vee A$ 和 $\neg P \vee B$，通过消解可以得到 $A \vee B$。
   >
   >**证明方法**
   >
   >为了证明这个问题的结论，我们需要用反证法。
   >
   >**反证法步骤**
   >
   >1. **假设反命题：** 存在一个子句 $C$，通过与 $\neg P \vee \neg Q$ 消解，可以得到一个正的单子句（即 $P$ 或 $Q$）。
   >2. **形式化子句：** 考虑子句 $C$ 的可能性：
   >   - 如果子句 $C$ 包含正字母（如 $P$ 或 $Q$），例如 $P \vee B$，我们希望通过与 $\neg P \vee \neg Q$ 消解出一个正的单子句。
   >3. **消解可能性分析：**
   >   - 假设子句 $C$ 是 $P$，那么消解的对象为 $\neg P \vee \neg Q$ 和 $P$。通过消解法则，我们消去互补的 $P$ 和 $\neg P$，得到 $\neg Q$。
   >   - 假设子句 $C$ 是 $Q$，那么消解的对象为 $\neg P \vee \neg Q$ 和 $Q$。通过消解法则，我们消去互补的 $Q$ 和 $\neg Q$，得到 $\neg P$。
   >4. **分析结果：** 通过上述分析，无论是消解 $P$ 还是 $Q$，结果都为否定子句 $\neg Q$ 或 $\neg P$，而不是一个正的单子句（即 $P$ 或 $Q$）。因此，消解无法得到任何正的单子句。
   >5. **反证成立：** 假设反命题是错误的，因此我们证明了不存在一个子句可以通过与 $\neg P \vee \neg Q$ 消解得到一个正的单子句。

   回溯排查消解路径：
   也即是找到一个满足如下的形式：

   ![true_atom](https://github.com/Linxin-Xv/logicgraph/blob/main/true_atom.png?raw=true)

   其中$P_1$为利用已有知识库消解过程中产生的序列中的一个子句，$P_2$为知识库中的一个子句。

   由引理1可知，单子句的上一步参与消解的字句长度不可能超过$2$个子句，所以$P_2$应该是我们的假设：$\neg UnCol$,$P_1$是$UnCol$。

   由于我们有假设$\neg UnCol$在知识库中，所以我们可以忽略$UnCol$项，因为他总是会被消解。

   同时，我们利用知识库中的事实来对每个字句进行初始的处理可以把知识库变成：
   $$
   1.  (R(a) \lor G(a) \lor B(a) ) \\
   2.  (R(b) \lor G(b) \lor B(b) ) \\
   3.  (R(c) \lor G(c) \lor B(c)) \\
   4.  (R(d) \lor G(d) \lor B(d) ) \\
   
   - 顶点 a 和 b 之间的边:\\
     1.  ( \neg R(a) \lor \neg R(b)  ) \\
     2.  ( \neg G(a) \lor \neg G(b) ) \\
     3.  ( \neg B(a) \lor \neg B(b) ) \\
   
   - 顶点 a 和 c 之间的边:\\
     1.  ( \neg R(a) \lor \neg R(c) ) \\
     2.  ( \neg G(a) \lor \neg G(c) ) \\
     3.  ( \neg B(a) \lor \neg B(c) ) \\
   
   - 顶点 a 和 d 之间的边:\\
     1.  ( \neg R(a) \lor \neg R(d) ) \\
     2.  ( \neg G(a) \lor \neg G(d) ) \\
     3.  ( \neg B(a) \lor \neg B(d) ) \\
   $$

   $$
   - 顶点 b 和 c 之间的边:\\
     1.  ( \neg R(b) \lor \neg R(c) ) \\
     2.  ( \neg G(b) \lor \neg G(c) ) \\
     3.  ( \neg B(b) \lor \neg B(c) ) \\
   
   - 顶点 b 和 d 之间的边:\\
     1.  ( \neg R(b) \lor \neg R(d) ) \\
     2.  ( \neg G(b) \lor \neg G(d) ) \\
     3.  ( \neg B(b) \lor \neg B(d) ) \\
   
        $$
   
        $$
   - 顶点 c 和 d 之间的边:\\
     1.  ( \neg R(c) \lor \neg R(d) ) \\
     2.  ( \neg G(c) \lor \neg G(d) ) \\
     3.  ( \neg B(c) \lor \neg B(d) ) \\
     - 顶点与连边信息
   V(a) ,V(b),V(c) ,V(d) \\
   E(a, b),E(a, c),E(a, d),E(c, b),E(d, b),E(c, d)\\
   $$
   
        
   
        **假设我们利用以上的知识库的$SLD$算法能推导出一个正项单子句 $R(a) $**：
   
        回溯排查消解路径：
   
        也即是找到一个满足如下的形式：
   
        ![true_atom](https://github.com/Linxin-Xv/logicgraph/blob/main/true_atom.png?raw=true)
   
        其中$P_1$为利用已有知识库消解过程中产生的序列中的一个子句，$P_2$为知识库中的一个子句。
   
        ​        由于$P_1$和$P_2$之间可以消解，且由引理1可知$P_1$和$P_2$最大字句长度为$2$可得这两个字句其中一个必定含有非，一个必定含有对应的正项。由于整理过后的知识库中长度为2的子句都是两个非的析取，由引理1可知他们不可能和字句消解后得到一个形如$R(x)$的正项。所以利用以上的知识库的$SLD$算法不可能推导出一个正项单子句 。
   
        **假设我们利用以上的知识库的$SLD$算法能推导出一个负项单子句 $ \neg R(a) $**：
   
        其中$P_1$为利用已有知识库消解过程中产生的序列中的一个子句，$P_2$为知识库中的一个子句。回溯排查消解路径：
   
        也即是找到一个满足如下的形式：
   
        ![false_atom](https://github.com/Linxin-Xv/logicgraph/blob/main/false_atom.png?raw=true)
   
        其中$P_1$为利用已有知识库消解过程中产生的序列中的一个子句，$P_2$为知识库中的一个子句。
   
        我们显然可以知道$P_2$是形如$( \neg G(a) \lor \neg G(b)  )$的字句。
   
        我们可以得知$P_1$需要是形如$(\neg G(a) \lor G(b) )$的字句，这样可以消解得到一个为非的单子句。
   
        如下图，我们可以证明考虑形如$(\neg G(a) \lor G(b) )$的字句的前一步推理是不可能回退到现有知识库的。也即是利用知识库的SLD算法是不可能获得形如$(\neg G(a) \lor G(b) )$的字句。

![pic1](https://github.com/Linxin-Xv/logicgraph/blob/main/pic1.jpg?raw=true)

​                                                                                       （图1）

证明过程详见图1，[点击获取原件](https://github.com/Linxin-Xv/logicgraph/blob/main/Backtracking%20Logic%20Generation%20Graph.pdf)(下载可获取高清PDF)箭头方向为当前字句在$SLD$算法推理的前一步字句，连线上的内容为该步推理所利用的知识库中的字句信息。由图可知无法通过$SLD$算法得到形如$(\neg G(a) \lor G(b) )$的字句，也即是在$SLD$算法下，当前的假设是错误的。

综上，在$SLD$算法和当前知识库下，不能实现消解$K_4$完全图的三色问题到单子句。

如果在字句库中加入一个点只能使用一种颜色的限制，也即是以下内容：
$$
¬R(a)∨¬G(a),¬R(a)∨¬B(a),¬G(a)∨¬B(a)\\
¬R(b)∨¬G(b),¬R(b)∨¬B(b),¬G(b)∨¬B(b)\\
¬R(c)∨¬G(c),¬R(c)∨¬B(c),¬G(c)∨¬B(c)\\
¬R(d)∨¬G(d),¬R(d)∨¬B(d),¬G(d)∨¬B(d)\\
$$
进一步地，我们可以证明加入这些进入知识库也并不能利用$SLD$算法消解得到单子句。

对于得到正的单子句，情况同上。

对于得到一个负的单子句，$P_2$还可能是形如$( ¬R(a)∨¬G(a) )$的字句。

此时$P_1$只能是形如$\neg R(a) \lor G(a)$的字句。

我们可以通过从$P_1$出发去按照$SLD$算法回溯来证明不存在一个$SLD$算法得到的消解序列会存在形如$\neg R(a) \lor G(a)$的字句。![pic2](https://github.com/Linxin-Xv/logicgraph/blob/main/pic2.jpg?raw=true)

​                                                                                 （图2）

证明过程详见图2，[点击获取原件](https://github.com/Linxin-Xv/logicgraph/blob/main/part 2.pdf)(下载可获取高清PDF)箭头方向为当前字句在$SLD$算法推理的前一步字句，连线上的内容为该步推理所利用的知识库中的字句信息。由图可知无法通过$SLD$算法得到形如$(\neg G(a) \lor G(b) )$的字句，也即是在$SLD$算法下，当前的假设是错误的。


通过这种回溯和排查的方式，证明了在现有的知识库中，不能通过$SLD$算法和消解原理得到单子句。原因是，消解过程中所需要的推导步骤都需要引入新的子句，这些子句在现有的知识库中并不存在。

### 总结

你的证明基于以下几个关键点：
- 通过回溯和排查消解的每一步，分析消解路径的依赖性。
- 每一条消解路径都需要引入新的子句，这些子句在现有知识库中并不能得到存在。
- 因此，在不引入新子句的情况下，现有知识库无法通过消解推导出单子句。

这种方法有效地证明了现有知识库的限制，并表明了消解推导过程在此问题中的局限性。