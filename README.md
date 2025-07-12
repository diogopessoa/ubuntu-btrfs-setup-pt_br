# Instalaçã do Ubuntu em Btrfs + Snapshots
Este Script cria os Subvolumes Btrfs (ainda no modo LiveCD/USB) e faz a configuração de Snapshots automáticos para Ubuntu 24.04 (ou superior) e sistemas derivados compatíveis. 


## O que o script faz

- Cria os subvolumes no Btrfs;
  - `@`, `@home`, `@log`, `@cache`, `@tmp`, `@libvirt`, `@Flatpak`
- Snapshots automáticos habilitados;
- Habilita entrada de snapshot no Grub;
- Instala e configura:
  - `snapper` snapshots;
  - `grub-btrfs` integra os snapshots na entrada do Grub
  - `btrfs-assistant` aplicação gráfica para gerenciar snapshot com Snapper


## Requisitos

- Ubuntu 24.04 ou superior instalado com:
  - Sistema de arquivos raiz em **Btrfs**
  - Partição **/boot** separada em ext4 (1GB)
  - (Opcional) Partição EFI se for UEFI (1GB)
- Execução do Script `ubuntu-btrfs-setu` no **Live CD/USB**, após a instalação do Ubuntu

## Instale o Ubuntu com Btrfs
Este exemplo de instalação foi usado o Ubuntu 25.04.

### Passo a Passo

1. **Preparação**
   - Crie um pendrive bootável com a ISO do Ubuntu.
   - Se necessário, desative o Secure Boot na BIOS/UEFI para evitar problemas na instalação.

2. **Iniciar instalação**
   - Dê boot pelo pendrive e escolha o idioma.
   - Selecione "Instalação manual" (particionamento manual).

3. **Criar partições na ordem correta**
   - Crie uma tabela de partições GPT no disco.
   - Crie a partição **/boot/efi**:
     - Tamanho: 1 GB
     - Formato: FAT32 (vfat)
     - Tipo: EFI System Partition
     - Ponto de montagem: `/boot/efi`
   - Crie a partição **/boot**:
     - Tamanho: 1 GB
     - Formato: ext4
     - Ponto de montagem: `/boot`
   - Crie a partição raiz **/**:
     - Use o restante do espaço disponível
     - Formato: Btrfs
     - Ponto de montagem: `/`

4. **A tabela de partições ficará assim:**
   - `/boot/efi` em FAT32 (vfat)
   - `/boot` em ext4
   - `/` em Btrfs

6. **Continuar a instalação**
   - Instale o sistema normalmente, mas NÃO reinicie.

7. **NÃO reinicie após a instalação**
   - Feche o instalador após a instalação
   - Abra o terminal e execute o Scritp


## Como usar o script

⚠️ Após a instalação do Ubuntu com Btrfs, NÃO reinicie!  
Copie o script para a pasta Downloads do LiveCD/USB.

### Descubra quais são suas partições

 Abra o terminal e execute o comando `lsblk -f`.

Procure algo como `sda` ou `nvme0n1`. Exemplo de saída:

```
sda     
├─sda1  vfat   /boot/efi
├─sda2  ext4   /boot
└─sda3  btrfs  /
```

### Agora que sabe qual o tipo das suas partições, torne o script executável:

```bash
sudo su
cd Downloads
chmod +x ubuntu-btrfs-setup-pt_br.sh
```

### Execute o script:

A ordem dos parâmetros deve ser: `/`  `/boot`  `/boot/efi`

```bash
sudo ./ubuntu-btrfs-setup-pt_br.sh sda3 sda2 sda1 # o exemplo aqui foi sda3->`/` sda2->`/boot` sda1->`/boot/efi`
```

### ✅ Concluído! Agora reinicie a máquina para usufruir do Ubuntu com Snapshots automáticos.
💡 Dica: Para verificar os subvolumes Btrfs, abra o **Btrfs Assistant** e vá em "Subvolumes" ou execute o **comando** `sudo btrfs subvolume list /`


## Licença

Este projeto está licenciado sob a [Licença MIT](https://github.com/diogopessoa/ubuntu-btrfs-setup-pt_br/blob/main/LICENSE).

