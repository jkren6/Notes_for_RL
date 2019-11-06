# Linear Value-function Geometry

This note is copied from [Zhihu](https://zhuanlan.zhihu.com/p/54784178).

为了更好理解 off-policy learning 的一些问题，考虑对函数逼近做一些抽象的分析。

设状态空间中的 state-value function 为映射 ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=v%3AS%5Cto+R) （大部分的$$v $$ 函数并没有具体意义，即不对应任何具体的 policy ） 

记状态空间为 ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=%5Cmathcal+S%3D%5C%7Bs_1%2Cs_2%2C%5Cldots%2Cs_%7B%7C%5Cmathcal+S%7C%7D%5C%7D) ，value function 则为向量 $$\left[v\left(s_{1}\right), v\left(s_{2}\right), \ldots, v\left(s_{|\mathcal{S}|}\right)\right]^{T}$$  。

简化起见，设 ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=%5Cmathcal+S%3D%5C%7Bs_1%2Cs_2%2Cs_3%5C%7D) ，参数 ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=%5Cmathbf%7Bw%7D%3D%28w_1%2Cw_2%29%5ET) ，此时 value function ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=%5Bv%28s_1%29%2Cv%28s_2%29%2Cv%28s_3%29%5D%5ET) 可看作一个三维空间中的点。而参数 ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=%5Cmathbf%7Bw%7D) 则能够通过一个二维子空间提供一个替代的坐标系，其线性组合而成的逼近函数 ![\[&#x516C;&#x5F0F;\]](https://www.zhihu.com/equation?tex=v_%7B%5Cmathbf%7Bw%7D%7D) 显然也在这个子空间内。







