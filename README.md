# Mini-Cloud Project

このプロジェクトは、VirtualBoxとAnsibleを使って
シンプルなプライベートクラウド環境（ミニクラウド）を構築するためのものです。

## 📦 プロジェクト構成

```
mini-cloud/
├── inventory
├── controller-setup.yml
├── compute-setup.yml
├── vars/
│    ├── main.yml
│    └── compute_vars.yml
├── templates/
│    ├── dnsmasq.conf.j2
│    ├── netplan.yaml.j2
│    └── compute-netplan.yaml.j2
```

## 🎯 目的
- VirtualBox上に複数VMを立ち上げ、内部ネットワークで相互接続
- ControllerノードによるDHCPサーバーとDNSサーバー構築
- 各VMへのホスト名設定とネットワーク設定の自動化
- 小規模なクラウド環境をエミュレート

## 🛠 使用技術

- Ansible
- VirtualBox
- Ubuntu Server (推奨)

## 🚀 セットアップ手順

1. **リポジトリをクローン**

```bash
git clone https://github.com/あなたのユーザー名/mini-cloud.git
cd mini-cloud/
```

2. **インベントリを編集**
各ノードのIPアドレス、ユーザー名をinventoryファイルで指定してください。

3. **Controllerノードをセットアップ**
```bash
ansible-playbook -i inventory controller-setup.yml
```

4. **Computeノードをセットアップ**
```bash
ansible-playbook -i inventory compute-setup.yml
```

5. **ホスト名と内部DNSで通信確認**
```bash
ping controller.mini-cloud.local
ping compute01.mini-cloud.local
ping compute02.mini-cloud.local
```


