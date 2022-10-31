# Ansible-playground
Playground for ansible with macOS to try ansible commands and modules.

Install Ansible
`brew install ansible`

## Ansible node with multipass

### Step1. Install [multipass](https://multipass.run/docs/how-to-guides#heading--install-multipass-)

For macOS simply
`brew install --cask multipass`

### Step2. Prepare ssh key

- Create ssh key 
`ssh-keygen -C vmuser -f multipass-ssh-key`

- Add your ssh public key `multipass-ssh-key.pub` to *cloud-init.yaml*

### Step3. Create multipass instance

`multipass launch bionic -n vm1 --cloud-init cloud-init.yaml`

### Step4. Check ssh connection

Get instance IP address
`multipass list`

ssh connect to VM
`ssh -i multipass-ssh-key vmuser@IP_ADDRESS`

### Step5. Add to Ansible inventory

replace VM1_IP_ADDRESS in *inventory* with vm1 IP address

## Ansible ad-HOC-command

```shell
# PING the target node
ansible webserver -m ping

# Apt Update (use --become to get permission)
ansible webserver -m apt -a update_cache=true --become

# Run shell
ansible webserver -m shell -a "echo hello world"
```

## Ansible playbook

```shell
# Run playbook
ansible-playbook playbook.yml

# Check nginx website
curl {{IP_ADDRESS}}

# Copy index.html to nginx (Modify anything in index.html)
ansible-playbook --tags copyweb playbook.yml
```

## Reference

- [Enable ssh access to multipass vms](https://dev.to/arc42/enable-ssh-access-to-multipass-vms-36p7)
- [Charmed by multipass (lightning speed vm creation with multipass)](https://sejuba.medium.com/charmed-by-multipass-lightning-speed-vm-creation-with-multipass-55f49ebdbb53)
- [Ansible #4 - 安裝篇[mac]](https://www.gss.com.tw/blog/ansible-4-%E5%AE%89%E8%A3%9D%E7%AF%87-mac)
- [現代 IT 人一定要知道的 Ansible 自動化組態技巧](https://chusiang.gitbooks.io/automate-with-ansible/content/05.how-to-practive-the-ansible-with-docker.html)
- [Ansible 介紹](https://ithelp.ithome.com.tw/articles/10191609)