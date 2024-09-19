当且仅当det(A) = 0 A 为奇异矩阵
for A（2 * 2）
det（A） = |A| = a11a22 - a12a21——矩阵的值

高位矩阵简化
det(A) = a11(a22a33 − a32a23) − a12(a21a33 − a31a23) + a13(a21a32 − a31a22)
-> a11A11 +a12A12+a13A13 
Mij = det(Mij) ——删除aij 所在的行列
Aij = (−1)i+j det(Mij)  ——删除aij 所在的行列,并加入符号
![[Pasted image 20231011151840.png]]


注：可以对任意位置进行以上操作
![[Pasted image 20231011151737.png]]

倒置矩阵的特性：（导致矩阵行列式和原矩阵相等）
If A is an n × n matrix, then det(AT ) = det(A).


行列式的性质：
(行列共用)
一，det（EA）= det（E）det（A）
type1：
——交换原矩阵行/列，则变号
type2： E乘k，det（EA）=kdet（A）
type3： E加c ，det（EA）=det（A）


二，当且仅当det(A) = 0 A 为奇异矩阵
三，det(EA) = det(E) det(A) = det(AE)

运用性质一进行化简：
![[Pasted image 20231011155205.png]]