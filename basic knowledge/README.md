# 整理面試的筆記

1.
物件導向的三大特性
封裝
將程式碼包裝成為Class以提供特定功能的一種過程。好處：程式碼共用。
繼承
Class可透過Inheritance(繼承)來擴充(或修改)內容。
多型
在執行階段，定義可供用戶端程式碼交換使用，具有不同功能但名稱完全相同之方法或屬性的Class。

another solution:
  我是一個封裝良好的工程師，因此許多細節妳不需要清楚了解，只要交給我去執行就好。　－＞封裝
  我畢業於國立清華大學資訊工程學系，有需多學長姐的經驗供我借鏡，因此我也繼承他們的經驗。　－＞繼承
  我興趣廣泛，喜歡學習，除了是軟體工程師，依據任務的需求也可以是前端工程師或者後端工程師甚至是資料分析師。　－＞多型

2.
Overload和Override的區別。Overloaded的方法是否可以改變 
返回值的類型? 

Overload發生在同一類別裡，Override發生在繼承關係間。 
Overload為靜態連結，Override為動態連結。 
可改變返回值的型態，前提是參數也要變，參數相同傳回值不同是
不被允許的。 

Overloading : 在同一個函數內，使用多個相同名稱但輸入參數不同的函數。  ＝ 給予太多工作 (load多到太over)。 
Overriding :  繼承父類別後，改寫父類別的方法。　＝　忤逆家長 (也就是ride在家長頭上太over的意思)。

3.
what is different between mutex and semaphore?

Mutex是一把鑰匙，一個人拿了就可進入一個房間，出來的時候把鑰匙交給隊列的第一個。一般的用法是用於串行化對critical section代碼的訪問，保證這段代碼不會被並行的運行。
(A mutex is really a semaphore with value 1.)

Semaphore是一件可以容納N人的房間，如果人不滿就可以進去，如果人滿了，就要等待有人出來。對於N=1的情況，稱為binary semaphore。一般的用法是，用於限制對於某一資源的同時訪問。

4.
Compare stack and queue

佇列(Queue)是用先進先出的方式處理物件的集合，例如到銀行排隊，先排的人先處理；
而堆疊(Stack )是後進先出的集合，例如玩撲克牌排遊戲時，發牌時是從整疊的最上一張拿取。


5.
write a function that can calculate 1*2+2*3+.....+(n-1)*n

int nc(int n){
 int sum = 0;
 for(int i = 2; i <= n; i++){
  sum = sum + n*(n-1);
 }
 return sum;
}

6.
Explain process and thread

Program：放在二次儲存裝置中，尚沒有被Load到記憶體的一堆Code
         稱之為「程式」。  (也就是還是死的)

Process：已經被Load到記憶體中，任何一行Code隨時會被CPU執行，且其宣告的在記憶體
         的變數的值會隨著需求而不斷變動。
         稱之為「程序」。 (也就是活的Program) => 恐龍本第三章
         一個多工作業系統(Multitasking Operating System)可以同時運行多個Process
         然而一個CPU一次只能做一件事情，但CPU的數量永遠少於運行中的Process數，
         因此每個Process使用的時間需要被排程(Scheduling) => 恐龍本第五章
         又每個Process間在記憶體中，如果擺放的方式不當，就會在記憶體中產生很多
         沒辦法用到的碎片，因此MemoryManagement是一個問題 => 恐龍本第八章
         另外，每個Process所需要的記憶體總合，也可能大於實體記憶體，因此需要另
         外用二次儲存裝置充當虛擬記憶體(Virtual Memory)，但是二次儲存裝置的速
         度肯定很慢，因此如何做到對虛擬記憶體最小的依賴，盡量避免Page Fault(電
         腦在主記憶體中找不到資料，而要去二次記憶體找，就稱為Page Fault)
         防止Thrashing的發生(因為Virtual Memory演算法不當，造成幾乎每次存取都要
         依賴二次記憶體，就是Thrashing)，以達到效能最佳化，也是個學問 => 第九章

Thread ：在同一個Process底下，有許多自己的分身，就是Thread，中文又翻成執行緒。
         以往一個Process一次只能做一件事情，因此要一面輸入文字，一面計算字數，
         這種事情是不可能的。但是有了Thread之後，可以在同一個Process底下，讓輸
         入文字是一個Thread，計算文字又是另外一個Thread，對CPU來說兩個都是類似
         一個Process，因此兩個可以同時做。
         又一個Process底下有數個Thread，而一個Process的Global Variable可以讓
         它的所有Thread共享，也就是所有Thread都可以存取同一個Process的Global
         Variable。而每個Thread自己也有自己的專屬Variable。 => 恐龍本第四章
         但是，如果有兩個Thread要存取同一個Global Variable，有可能發生問題，
         也就是說可能會存取到錯的值(例如兩個Thread同時要對一個Variable做加減，
         最後那個答案可能會是錯的)，這就是Synchronization問題 =>恐龍本第六章
         又，每一個Thread之間可能會互搶資源，而造成死結(Deadlock)，只要以下四
         個條件都滿足就有死結。(1)這個資源不能同時給兩個人用 (2)有一個人拿了一
         個資源，又想拿別人的資源 (3)如果一個人占了茅坑不拉屎，占用資源很久，仍
         不能趕他走 (4)A等B，B等C，C等D，D又等A 等成一圈。 要解決這種狀況有
         Avoid(預防) 或 避免(Prevent)兩種方式，破除以上四種其中一種即可。
         => 恐龍本第七章

7.
Deadlock Def：
一組processes陷入互相等待的情況(Circular waiting)
造成processes接無法往下執行，使得CPU utilization及Throughput大幅降低

8. 
Deadlock vs Starvation

Deadlock           | Starvation  
---------------|--------
一組processes形成circular waiting，導致processes無法往下執行|某(些)processes形成infinite Blocking ∵長期無法取得完成工作所需資源    
不允許資源preemptive    | 易發生在不公平、preemptive的環境    
CPU utilization及Throughput會大幅下降    | 與此無關聯    


	
9.
Deadlock成立的四個必要條件
Mutual exclusion(互斥)
Def：
資源在同一時間內，至多只允許一個process使用(不允許≥2個processes同時使用)
其它欲使用此resource的process必須wait，直到該process釋放resource為止
eg. printer、Disk、CPU etc.
eg. 不具mutual exclusion→Read-only File
Hold & wait(持有並等待) (Partial Allocation)
Def：
process持有部分資源且又在等待其它processes所持有的資源
No preemption(不可強取豪奪)
Def：
process不可搶奪其它waiting process所持有的資源，除非其自願釋放
Circular waiting(循環等待)
Def：
存在一組process
P0→P1→P2→...→Pn→P0
P0~Pn形成Circular waiting
	
	