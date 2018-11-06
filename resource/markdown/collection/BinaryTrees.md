![tree](https://images.pexels.com/photos/22138/pexels-photo.jpg?auto=compress&cs=tinysrgb&h=350)

<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">一、树</h3>

> 浩瀚宇宙，从 **点** 到**线**，**线**到**面**，**面**到**体**，组成了丰富多彩的世界。动物、植物和其他物体正是存储在 **宇宙** 这个数据结构中。
>
> 前几篇[文章](https://github.com/about-cloud/JavaCore)介绍了 **线性** 的数据结构: `ArrayList`、`LinkedList`及其组合`HashMap`。**线性** 数据结构到 **非线性** 数据结构，就像 **树干** 发叉一样：

![line to tree]()

> 从数据结构进化的角度来看，:palm_tree:**树(tree)** 的生成是 **链表** 进化而来。**链(Linked)**  每个节点最多只有一个 **前驱节点** ，那么可以称这个 **链** 为 🌴**树(tree)** 。数据结构中的树就像一颗倒挂的树。

![line to tree]()

>  **链表** 只不过是特殊的树，就像树没有树枝只有树干一样。

#### 数的基本术语

![tree]()

1.  **节点(Node)**：树中的每个元素称为 节点(Node)；
2. **根结点(Root Node)**：树最顶端的节点被称为根结点（树根），根结点无父节点；
3. **父节点(Parent Node)**：节点的（上面的）前驱节点在树中被称为父节点；
4. **子节点(Child Node)**：（下面的）后继节点被称为子节点；
5. **子树(Subtree)**：子节点及其下面的节点组成的树称为子树 ；
6. 一棵树最多只有一个根节点，树中的每个子节点最多只有一个父节点；
7. **节点的度**：一个节点含有的子树的个数称为该节点的度（叶子节点的度为0）；
8. :leaves:**叶节点(Leaf Node)**（叶子节点或终端节点）：度为0的节点称为叶节点（也就是没有子节点的节点称为叶子节点）；
9. **非终端节点** 或分支节点：度不为0的节点（拥有子节点的节点）；
10. **兄弟节点**：具有相同父节点的节点互称为兄弟节点；
11. **树的度**：一棵树中，节点中最大的度称为树的度；
12. **节点的层次**：从根开始定义起，**根为第1层**，根的子节点为第2层，以此类推；
13. **树的高度或深度**：树中节点的最大层次；
14. **堂兄弟节点**：双亲在同一层的节点互为堂兄弟；
15. **节点的祖先**：从该节点上溯至根节点，所经分支上的所有节点；
16. 子孙节点：该节点下面所有所有的节点称为该节点的子孙节点；
17. 空树：没有节点的树称为空树；
18. **森林**：由多棵互不相交（没有重叠节点）的树组成的集合称为森林（单棵树可以认为是特殊的森林）；



<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">二、二叉树</h3>

> **二叉树**是每个节点最多只有两个子树的树。子树通常被称为**左子树(Left subtree)**和**右子树(Right subtree)**。

![BinaryTree]()

#### 二叉树的特性

1. 在非空二叉树的 `i` 层上，至多有  **$$2^{i-1}$$**个节点`(i>=1)`；
2. 在深度为 `d` 的二叉树上最多有 `2d-1` 个结点`（d>=1)`;
3. 对于任何一棵非空的二叉树,如果叶节点个数为 `n0`，度数为 `2` 的节点个数为 `n2`，则有: `n0 = n2 + 1`。

#### 二叉树的遍历

>  **二叉树遍历**：从树的根节点出发，按照某种 **次序** 依次访问二叉树中所有的节点，使得每个节点被访问仅且一次。

这里有两个关键词：**访问** 和 **次序**。**访问** 包括 **增删改查**， **次序** 包括 **前序**、**中序**、**后序**，`前中后`是以树的根节点作为参照物:triangular_flag_on_post:。

#### 1、前序遍历



#### 2、中序遍历



#### 3、后序遍历



<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">三、最优二叉树（哈夫曼树）</h3>





<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">三、平衡二叉树</h3>





<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">四、二叉查找树</h3>





<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">五、AVL树</h3>





<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">六、红黑树</h3>



<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">七、B-Tree和B+Tree</h3>

> 这种和MySQL的[InnoDB索引](https://github.com/about-cloud/JavaCore)息息相关，单独拿出一个章节去讲解，详见：
>
> https://github.com/about-cloud/JavaCore