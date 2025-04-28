# Mini-Cloud Project

このプロジェクトは、VirtualBoxとAnsibleを使って
シンプルなプライベートクラウド環境（ミニクラウド）を構築するためのものです。

## 📦 プロジェクト構成

```
mini-cloud/
├── inventory
├── controller-setup.yml
├── compute-setup.yml
├── create-vm.yml              # VirtualBox上にVMを作成するPlaybook
├── vars/
│    ├── main.yml
│    ├── compute_vars.yml
│    └── vm_list.yml           # VMスペックを定義する変数ファイル
├── templates/
│    ├── dnsmasq.conf.j2
│    ├── netplan.yaml.j2
│    └── compute-netplan.yaml.j2
├── README.md
```

## 🎯 目的

- VirtualBox上に複数VMを立ち上げ、内部ネットワークで相互接続
- ControllerノードによるDHCPサーバーとDNSサーバー構築
- 各VMへのホスト名設定とネットワーク設定の自動化
- 小規模なクラウド環境をエミュレート

## 🚀 セットアップ手順

### 仮想マシンの作成

1. `vars/vm_list.yml`でVMのスペックを定義
2. 以下のコマンドでVirtualBoxにVMを作成

```bash
ansible-playbook -i localhost, create-vm.yml
```

### コントローラーとコンピュートノードのセットアップ

それぞれVMが起動したら、以下のPlaybookを順番に実行します。

```bash
ansible-playbook -i inventory controller-setup.yml
ansible-playbook -i inventory compute-setup.yml
```

## 🌟 特徴

- すべてAnsibleで一括構成管理
- ネットワーク/ホスト名設定も自動化
- プライベートクラウドの基本概念を実践的に学べる
- 拡張すればさらに大規模なクラウド環境も構築可能

## 📚 ライセンス

MITライセンス

---

# 🙌 コントリビューション歓迎！

バグ報告、プルリクエスト大歓迎です！

Let's build the mini-cloud together! 🚀
