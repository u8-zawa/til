# Quick Start

このガイドは、root（管理者）権限を持つコンピュータで SingularityCE を実行するためのもので、SingularityCE をソースコードからインストールします。

## インストール方法

SingularityCE をネイティブに実行するには、Linux システムが必要です。

### 依存関係をインストール

Debian 系 Linux

```
# リポジトリが最新であることを確認する
sudo apt-get update
# 依存関係のdebianパッケージのインストール
sudo apt-get install -y \
   wget \
   build-essential \
   libseccomp-dev \
   libglib2.0-dev \
   pkg-config \
   squashfs-tools \
   cryptsetup \
   runc
```

RHEL 系 Linux

```
# コンパイル用の基本的なツールのインストール
sudo yum groupinstall -y 'Development Tools'
# 依存関係のRPMパッケージのインストール
sudo yum install -y \
   wget \
   libseccomp-devel \
   glib2-devel \
   squashfs-tools \
   cryptsetup \
   runc
```

SingularityCE のインストールには、大まかに 3 つのステップがあります。

1. Go のインストール
2. SingularityCE のダウンロード
3. SingularityCE のソースコードのコンパイル

### Go のインストール

SingularityCE は Go で書かれており、お使いのディストリビューションのリポジトリにある Go よりも新しいバージョンの Go が必要な場合があります。[公式サイト](https://go.dev/dl/)から最新版の Go をインストールすることをお勧めします。

[Go のダウンロードページ](https://go.dev/dl/)にアクセスし、お使いの環境に適したパッケージアーカイブを選択します。ダウンロードが完了したら、アーカイブを`/usr/local`に展開します（または、go のインストールページにある他の手順を使用します）。または、こちらのコマンドに従ってください（必要に応じて、値を置き換えてください）

[Go のダウンロードページ](https://go.dev/dl/)から選択し、適したパッケージアーカイブをダウンロードして`/usr/local`に展開します。以下のコマンドを使用することができます。（値は適宜、書き換えてください）

```
export VERSION=1.20.2 OS=linux ARCH=amd64 && \
  wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
  sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
  rm go$VERSION.$OS-$ARCH.tar.gz
```

環境変数`PATH`に Go を設定します

```
echo 'export PATH=/usr/local/go/bin:$PATH' >> ~/.bashrc && \
  source ~/.bashrc
```

### SingularityCE のダウンロード

SingularityCE は、いずれかのリリースからダウンロードできます。全リストを見るには、GitHub のリリースページをご覧ください。インストールするリリースが決まったら、以下のコマンドを実行してインストールを進めてください。（バージョンの値は適宜、書き換えてください）

```
export VERSION=3.11.1 && \
    wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-ce-${VERSION}.tar.gz && \
    tar -xzf singularity-ce-${VERSION}.tar.gz && \
    cd singularity-ce-${VERSION}
```

### SingularityCE のソースコードのコンパイル

これで SingularityCE をビルドする準備ができました。依存関係は自動的にダウンロードされます。以下のコマンドで SingularityCE をビルドすることができます

```
./mconfig && \
    make -C builddir && \
    sudo make -C builddir install
```
