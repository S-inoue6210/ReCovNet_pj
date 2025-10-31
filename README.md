# ReCovNet（再現・拡張版）

このリポジトリは、論文  
**「ReCovNet: Reinforcement learning with covering information for solving maximal coverage billboards location problem」**  
（Zhong et al., 2024, *International Journal of Applied Earth Observation and Geoinformation*）  
で提案されたモデルの **再現および検証を目的として構築された独自実装** です。  

本リポジトリは **元の著者による公式リポジトリではなく**、研究目的で再整理・補足を行った派生版です。

---

## 元論文情報

Zhong, Y., Wang, S., Liang, H., Wang, Z., Zhang, X., Chen, X., & Su, C. (2024).  
ReCovNet: Reinforcement learning with covering information for solving maximal coverage billboards location problem.  
*International Journal of Applied Earth Observation and Geoinformation*, 128, 103710.  
[[論文リンク]](https://www.sciencedirect.com/science/article/pii/S1569843224000645)

```bibtex
@article{zhong2024recovnet,
  title={ReCovNet: Reinforcement learning with covering information for solving maximal coverage billboards location problem},
  author={Zhong, Yang and Wang, Shaohua and Liang, Haojian and Wang, Zhenbo and Zhang, Xueyan and Chen, Xi and Su, Cheng},
  journal={International Journal of Applied Earth Observation and Geoinformation},
  volume={128},
  pages={103710},
  year={2024},
  publisher={Elsevier}
}
```

---

## 環境構築手順

本コードは **Python 3.7** でのみ動作確認されています。
以下の手順で仮想環境をセットアップしてください。

```bash
conda env create -f environment.yml
```

> ⚠️ GPU環境を使う場合は、上記の conda install コマンドで CUDA 対応版 PyTorch をインストールしてください。
---

## ディレクトリ構成

```text
project_root/
├─ data/                    # データセット
├─ nets/                    # ネットワークの定義
├─ output/                  # 学習済みモデル・結果出力
├─ problems/                # 問題の定義
├─ utils/                   # その他コード
├─ environment.yml
├─ MCBLP_DRL_NY.ipynb       # NY市データに対する推論実行Notebook
├─ options.py               # モデル学習の設定管理
├─ train.py                 # 強化学習の実装
└─ README.md
```

---

## 実験フロー概要

1. **データ準備**
   論文で使用された MCBLP（Maximal Coverage Billboard Location Problem）のデータセットを用意します。

   * `data/` に `.pkl` 形式のファイルを配置します。
   * 各データには座標（`POINT_X`, `POINT_Y`）および需要情報が含まれます。

2. **正規化処理**
   全データを座標スケールで正規化します（`Normalization()` 関数を利用）。

3. **推論実行**
   `epoch-499.pt` などの訓練済みモデルをロードし、全データに対して推論を実施します。

4. **評価・可視化**

   * 各施設の配置結果とカバレッジ率を算出
   * matplotlib でビルボード配置の最適化結果を描画
   * 論文の報告値（GA, Gurobi, AM）と比較可能なメトリクスを出力

---

## ⚠️ 免責事項

* 本リポジトリは **元著者とは無関係の再現実装** です。
* 研究・教育・非商用利用を目的としており、精度・再現率の完全性は保証しません。
* 引用の際は必ず元論文を参照してください。

---