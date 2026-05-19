# Restaurar este backup en otro PC

## Requisitos
- Linux Mint Xfce recién instalado
- Conexión a internet
- Este repositorio clonado

## Instrucciones para la IA (opencode)

Cuando le pase este archivo a la IA, debe ejecutar esto en orden:

### 1. Clonar el repo (si no está clonado)
```bash
git clone https://github.com/Ivan-error404/Mint_xfce_-.git ~/mint-restore
cd ~/mint-restore
```

### 2. Restaurar paquetes (2721 apps)
```bash
sudo apt update
sudo dpkg --set-selections < paquetes.txt
sudo apt dselect-upgrade
```

Si hay errores de dependencias:
```bash
sudo apt --fix-broken install
```

### 3. Restaurar configuraciones de Xfce
```bash
cp -r mint-backup/xfce4 ~/.config/
cp -r mint-backup/Thunar ~/.config/
cp -r mint-backup/gtk-3.0 ~/.config/
cp -r mint-backup/autostart ~/.config/
```

### 4. Restaurar atajos de teclado
```bash
cp mint-backup/xfce4-keyboard-shortcuts.xml ~/.config/xfce4/xfconf/xfce-perchannel-xml/
```

### 5. Restaurar dotfiles
```bash
cp mint-backup/.bashrc ~/ 2>/dev/null
```

### 6. Restaurar imágenes (90 MB)
```bash
cp -r mint-backup/mis-imagenes ~/Imágenes
```

### 7. Restaurar lanzadores personalizados
```bash
mkdir -p ~/.local/share/applications
cp -r mint-backup/app-launchers/* ~/.local/share/applications/ 2>/dev/null
```

### 8. Restaurar temas, iconos y fuentes (si existen)
```bash
[ -d mint-backup/temas ] && cp -r mint-backup/temas ~/.themes
[ -d mint-backup/iconos ] && cp -r mint-backup/iconos ~/.icons
[ -d mint-backup/fuentes ] && cp -r mint-backup/fuentes ~/.fonts
```

### 9. Restaurar Flatpak (Anytype)
```bash
flatpak install flathub io.anytype.anytype -y 2>/dev/null
```

### 10. Aplicar cambios
```bash
xfce4-panel -r 2>/dev/null
```

Cerrar sesión y volver a entrar para que todo se aplique correctamente.

## Notas
- Si la GPU es diferente, abrir Driver Manager e instalar drivers adicionales
- Los lanzadores de web apps (Claude, Proton Mail) usan Brave como base, instalar Brave si no está: `sudo apt install brave-browser`
- Para más detalles de cada atajo y configuración, ver `manual-fallback.txt`
- Si algo no queda igual, el backup completo está en `mint-backup-completo.tar.gz`
