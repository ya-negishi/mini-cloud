# Mini-Cloud Project

このプロジェクトは、VirtualBoxとAnsibleを使って
シンプルなプライベートクラウド環境（ミニクラウド）を構築するためのものです。  
さらに、PXEブートを使ったネットワークインストールも自動化しています！

---

## 📦 プロジェクト構成

```
mini-cloud/
├── cloud-init/
├── pxe-menu/
│    └── pxelinux.cfg/
│         └── default
├── 01_create-vm.yml
├── 02_controller-setup.yml
├── 03_pxe-setup.yml
├── 04_compute-setup.yml
├── vars/
├── templates/
├── inventory
├── README.md
```

---

## 🎯 プロジェクトの目的

- VirtualBox上に仮想マシンを作成
- ControllerノードをDHCP/DNS/PXEサーバー化
- PXEブートでComputeノードを無人インストール
- ミニクラウド基盤の基本概念を実践的に学習
- Ansibleによるインフラ自動化の体験

---

## 🛠 セットアップ手順

### ① 仮想マシンの作成

```bash
ansible-playbook -i localhost, 01_create-vm.yml
```

---

### ② Controller VMにUbuntuインストール

01_create-vm.yml実行後、VirtualBoxマネージャーで

1. controller VMを選択
2. ストレージ設定からUbuntuインストールISOをマウント
3. controller VMを起動
4. Ubuntuインストーラーで通常インストール
   - SSHサーバーをインストールするオプションにチェック
   - ネットワークは一旦DHCPのままでOK
5. インストール完了後、controllerにSSHログインできることを確認

---

### ③ Controllerノードの基本セットアップ

```bash
ansible-playbook -i inventory 02_controller-setup.yml
```

これにより、
- DHCP/DNSサーバー構築
- PXEブート環境構築
- HTTPサーバー公開

が自動で行われます。

---

### ④ ComputeノードのPXEブートと自動インストール

1. Compute01, Compute02をPXEブート設定にする
2. 起動するとPXEメニューが表示される
3. 対応するインストールメニューを選択すると無人インストール開始！

---

### ⑤ Computeノードの最終セットアップ

```bash
ansible-playbook -i inventory 04_compute-setup.yml
```

---

## 🌟 特徴

- すべてAnsibleによる構成管理
- ネットワーク/ホスト名設定自動化
- PXEブートによるゼロタッチインストール
- 再現性・拡張性の高いインフラ設計

---

## 📚 ライセンス

MITライセンス

---

# 🙌 コントリビューション歓迎！

バグ報告、プルリクエスト、機能提案お待ちしています！

Let's build the mini-cloud together! 🚀
