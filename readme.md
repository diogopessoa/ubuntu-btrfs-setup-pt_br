# Ubuntu Btrfs Setup Script

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
- Execução no **Live CD/USB**, após a instalação do Ubuntu

## Como usar o script

1. Após a instalação do Ubuntu com Btrfs, NÃO reinicie! só clique em fechar o instalador.
2. Copie o script para o LiveCD/USB.
2. Torne-o executável:

```bash
chmod +x ubuntu-btrfs-setup.sh
```

3. Execute como root (ou via `sudo`):

```bash
sudo ./ubuntu-btrfs-setup.sh sda3 sda2 sda1
```

Onde:

- `sda3` é a partição **/ (root)** em Btrfs (todo o restante do espaço)
- `sda2` é a partição **/boot** em ext4 (1GB sugerido)
- `sda1` (opcional) é a partição **/boot/efi** em vfat (1GB sugerido)

> A ordem dos parâmetros é importante: ROOT / BOOT / EFI


## Licença

Este projeto está licenciado sob a Licença MIT.

## Tags

`Ubuntu` `Btrfs` `Snapper` `Snapshots` `grub-btrfs` `btrfs-assistant` `fstab` `subvolumes` `Linux` `Debian`

