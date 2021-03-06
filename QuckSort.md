#快速排序 Wiki
## 原理
快速排序使用分治法（Divide and conquer）策略来把一个序列（list）分为两个子序列（sub-lists）。

步骤为：
- 从数列中挑出一个元素，称为"基准"（pivot），
- 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作。
- 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。

递归的最底部情形，是数列的大小是零或一，也就是永远都已经被排序好了。虽然一直递归下去，但是这个算法总会结束，因为在每次的迭代（iteration）中，它至少会把一个元素摆到它最后的位置去。

![快速排序算法示意图](/images/quick_sort.png)

## 子系列切分
使用基准pivot（数组的第一个元素）进行切分，小于pivot的放在左边，大于pivot放到右边。
```java
private static int partition(int a[], int lo, int hi){
        int l = lo, r = hi+1;   //左右扫描指针
        int pv = a[lo];         //切分基准元素
        int tmp = 0;
        while (true){
            while (a[++l] < pv) if (l == hi) break;
            while(pv < a[--r] ) if (r == lo) break;
            if (l >= r) break;
            //交换位置
            tmp = a[r];
            a[r] = a[l];
            a[l] = a[r];
        }
        // 将 pv 放入正确位置
        a[lo] = a[r];
        a[r] = pv;
        // a[lo..r-1] <= a[r] => a[r+1..hi] 达成
        return r;
    }
```
![切分规矩图](/images/quich_sort_1.png)


#参考
- 《算法（第4版）》