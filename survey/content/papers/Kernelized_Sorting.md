---
title: "kernelized_Sorting"
date: 2020-10-20T06:40:05+09:00
draft: true
---


# Kernelized_Sorting
## Link:
https://papers.nips.cc/paper/3608-kernelized-sorting
## Authors:
Novi Quadrianto, Le Song, Alex J. Smola
## part of:
Advances in Neural Information Processing Systems 21 (NIPS 2008)
<!-- ## 投稿日付 -->

---

# Abstract
物体のマッチング検出には、基本的に物体のクラス間での類似度の指標を必要とするが、この研究では各クラスの内の類似度で完結する
これはペア間の独立性(Hillbert Schmidt Independence Criterion)の平均を最大化することで達成されている
これにより、特殊な構造を持つ二次代入問題(quadratic assignment problem)に落とし込み、局所解をシンプルなアルゴリズムで解決できる

---

## 1 Introduction
教師なし学習においてマッチングするペアを見つけることこそが重要な要素となりうる
例:写真と人物紹介のテキスト、地図と衛星画像、楽譜と演奏などなど
こんなとき、片方をもう片方へと変換する関数が欲しくなる
よく使われる方法には、事前知識を用いるか、共起性の持つことによって互換性のスコアを決定するなどがある

とはいえ、そのような一致が存在しなかったり事前に得られないこともある
つまり、それぞれXとYについて理解していても(the sources of observations,say X and Y,)、その対応(mapping)を理解していない可能性がある
例えば、別の言語で書かれた同じ内容の文書があるとき、この二つの対応関係を見つけることがゴールとなる

この研究では、クロスドメインの類似度指標のいらない手法を提案する

この手法は、領域横断写像(cross-domain mapping)を知らなくてもランダム変数空間の依存性(dependence)を推定できるという事実によるものである

二つのセット間のヒルベルト・シュミット独立基準を選択して、最大化するものを探す
副作用として、共分散の明示表現を得る

この手法がソートを一般化することを示し、相互情報量の近似のような、異なる依存性を用いるとき[^1]のアルゴリズムに関連する

最後に、カーネル化ソート(kernelized sorting)のための簡単な近似アルゴリズムを示す

---

### 1.1 Sorting and Matching
空間X、Yの中のそれぞれx、yについて関係性を見つけたい
これについてパーミュテーションで目的関数を最大化するものを見つける
この論文では目的関数にヒルベルト・シュミット独立性基準と相互情報(Mutual Information)を試した

---

## 2 Hilbert Schmidt Independence Criterion
XとYが確率分布$Pr_{xy}$に存在するとする
ヒルベルト・シュミット独立性基準(以下HSIC)[^2]は、x-y間の依存度をヒルベルト空間に上のX、Yの存在するドメイン間の交差共分散のノルムを計算することによって測る
ヒルベルト空間が普遍的(universal)の時、xとyは独立しているときノルムは消失する
この値が大きいとカーネルの選択に強い依存性があることを示す

形式的にいうとFをX上のカーネルK:$\ki x \ki$と関連づけられた、Reproducing Kernel Hilbert Space(RHKS)
TODO: 飛ばす

---

## 5 Applications
アルゴリズムの評価

---

## 5.1 Data Visualization
データを可視化したい、このようなニーズは画像や文書の高次元データあ扱うときにおきがち
低次元オブジェクトの可視化には様々な方法があるが一様ではない
クラスター構造を明らかにするのに便利ではあるが、サイズに限りもある

kernelized sortingを使うとオブジェクト$x_i$間の類似表ｗあカーネル行列Lが与えられる
一方でカーネルKはオブジェクトを整列させるための類似度を表す

この研究ではガウスシアンRBFカーネルを簡単のため使った
これは最適ではない場合も当然ある、関数を選択するよりそれで何が得られるかを強調したいらしい

フリッカー画像248枚を40x40にダウンサンプリングして、RGかからLab color spaceに変換した40x40x3次元のデータを扱う

Xに対応するグリッドが”NIPS 2008”で、これに画像をレイアウトする
ソートして一致する座標に設置したのが図1

32枚たして320枚にして比較のために、SOM(Self-Organizing Map)とGTM(Generative Topographic Mapping)を使ったものをおまけに載せた

---

## 5.2 Matching
### Image matching
画像を20x40に分割して右半分と左半分に分ける
このデータセットの中から合うものを見つけられる順列(permutaion)を見つける

### Estimation
UCIのデータを使った
データの次元を二つに割って片方を並び替えて、生成したデータをマッチングさせ性能を推定誤差を使ってクオリティを測る
つまり、観測している$X_i$と$y_i$が関連していると仮定すると$y_i$と$y_{\pi(i)}$を2値分類かマルチクラス分類か回帰で比較することができる

高い依存性を持つように相関を確保するべく分割を行う
つまり高い相関係数を持つ次元を参照して分割する

相関が0以上の座標を選びそれらを等分して集合Aと集合Bとする
また余剰座標を二つの集合から均等に分割し、参照座標を集合Aに入れる

これにより、集合Bの次元が集合Aの少なくとも一つの次元に強い相関を持っていることがわかる
結果が表1
TODO: 以下飛ばす

### Multilingual Document Matching
多言語文書のマッチングにこの手法を用いる
目標は、非英語文書(ソース)と英語翻訳(ターゲット)を対応させることである
実際には対語辞書をkernelized sortで作成することもできる

カーネルとしてシンプルなTF-IDFを使った。

---

## 6 Summary and Discussion
このペーパーではマッチするペアと観測値(observations)間の依存性(dependency)をヒルベルト・シュミット独立性基準を用いて最大化することでソートを一般化した

これにより、領域横断的な類似度を必要とせずマッチングを行うことができ、このソートアルゴリズムでデータ可視化や多言語文書のマッチングなどまで多くの事例に効果的である

---

## References
- [^1]: T. Jebara.   Kernelizing sorting,  permutation,  and alignment for minimum volume PCA.   InConference on Computational Learning Theory (COLT), volume 3120 ofLNAI, pages 609–623. Springer, 2004.
- [^2]: A.J. Smola,  A. Gretton,  L. Song,  and B. Sch ̈olkopf.   A hilbert space embedding for distri-butions.   In E. Takimoto, editor,Algorithmic Learning Theory, Lecture Notes on ComputerScience. Springer, 2007.
- [^3]: K. Fukumizu, F. R. Bach, and M. I. Jordan.  Dimensionality reduction for supervised learningwith reproducing kernel Hilbert spaces.J. Mach. Learn. Res., 5:73–99, 2004.
- [^4]: T. Pham Dinh and L. Hoai An.   A D.C. optimization algorithm for solving the trust-regionsubproblem.SIAM Journal on Optimization, 8(2):476–505, 1988.
- [^5]: A.L. Yuille and A. Rangarajan. The concave-convex procedure.Neural Computation, 15:915–936, 2003.
- [^6]: R. Jonker and A. Volgenant. A shortest augmenting path algorithm for dense and sparse linearassignment problems.Computing, 38:325–340, 1987.
- [^7]: T. Cour, P. Srinivasan, and J. Shi.  Balanced graph matching.  In B. Sch ̈olkopf, J. Platt, andT. Hofmann, editors,Advances in Neural Information Processing Systems 19, pages 313–320.MIT Press, December 2006.
- [^8]: W.  Gander,  G.H.  Golub,  and  U.  von  Matt.   A  constrained  eigenvalue  problem.   InLinearAlgebra Appl. 114-115, pages 815–839, 1989.
- [^9]: P. Koehn. Europarl: A parallel corpus for statistical machine translation. InMachine Transla-tion Summit X, pages 79–86, 2005.
- [^10]: W. A. Gale and K. W. Church.   A program for aligning sentences in bilingual corpora.   InMeeting of the Association for Computational Linguistics, pages 177–184, 1991

---

### new words
- quadratic assignment problem
- Hillbert Schmidt Independence Criterion
  ヒルベルト-シュミット独立基準
  特性的な正定値カーネル(ガウシアンカーネル)による相互共分散作用素を用いて確率変数の独立性や依存性を調べる方法(?)
- cross-domain mapping
- if and only if
  必要十分条件
- Lab color space
