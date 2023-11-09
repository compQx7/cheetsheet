# venv
Pythonが既に入っていてVSCodeで開発する。
まずは好きなディレクトリを用意しその中で仮想環境を作成する。
python3 -m venv [env_name]
VSCodeで仮想環境を選択できるようにするために設定を加える。User Settingのvenv pathで仮想環境ディレクトリがあるパスを追加する。
VSCodeのウィンドウをreloadして、インタープリタ選択で仮想環境が選択できるようになる。
VSCodeターミナルも起動し直して完了。

# Python 環境 （古い）
> venvインストール
sudo apt-get install python2-venv
> 仮想環境フォルダ作成
python2 -m venv [virtual env name]
> 仮想環境アクティベート
. [virtual env name]/bin/activate
> 仮想環境ディアクティベート
deactivate
> 仮想環境削除（フォルダごと削除）
rm -rf [virtual env name]
> パッケージ（ライブラリ）インストール
pip install [package name]
> 現環境のパッケージリスト確認
pip list

# Python Anaconda（古い）
> 環境確認
conda info -e
> 仮想環境作成
conda create -n [env name]
> アクティベート
conda activate [env name]
> ディアクティベート
conda deactivate
> install ,conda installとpip installは同環境内で併用してはいけない
conda install [package name]
