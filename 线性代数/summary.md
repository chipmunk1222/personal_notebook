
1.[[方程求解]]：
	原矩阵（增广矩阵）->（三种变换）->行阶梯型矩阵->(消成简化行阶梯型)->简化行阶梯型——更易于看出方程解
2.[[矩阵的逆]]
	证明矩阵非奇异（有逆）：
	AB = BA = I
3.[[行列式计算]]
	初等矩阵（I经过一次（三大）变换得到的矩阵）
	左乘：初等行变换
	右乘：初等列变换
4.[[向量空间性质]]
	子空间：非空，$S\in V,x\in S,y\in S,x+y\in S,ax\in S->$S是V子空间
	零空间：Ax = 0 ->x为A的零空间（运用其次方程求解）
	生成集（spanning set）：$\sum_{i=1}^nc_iv_i=\forall \vec x\in V$
	线性无关证明:$\sum_{i=1}^nc_iv_i=0, \forall c_i=0$
	基生成：线性无关，生成空间V
	基转换：u为e坐标下表示的矩阵，u下坐坐标转e下坐标->乘u
	行空间，列空间
5.[[线性变换]]
	线性转换判定：$L(\alpha v_1+\beta v_2)=\alpha L(v_1)+\beta L(v_2)$
	kernel：核：$ker(L)=\{v\in V|L(v)=0\}$
	range：值域：$L(S)=\{w\in W|L(v)=w\}$
	求变换矩阵
	矩阵相似：B = S-1AS（B为新基下转置矩阵，S为基矩阵下B矩阵的表示（回式））
6.[[正交矩阵]]：
	xTy = ||x||||y||cosα   ->xTy = 0->正交（x⊥y）
	y⊥：y的正交补->所有y⊥x中所有x的集合（$N(y^T)$）
	正交集合：每一个向量正交且线性无关
	orthomnomal：单位正交向量
	orthogonal：正交向量
	矩阵内积：点乘
	正交矩阵：单位正交向量集合->QTQ = I
7.[[特征向量]]：
	Ax = λx
	求特征值，特征向量(A-λ）x  = 0 ->det(A-λI) = 0 ->λ，->(代入原式)->x
	特征空间：所有特征向量的集合
	对角化：S-1AS(S为特征值的矩阵) = ▲ ->S-1A^nS = ▲^n




