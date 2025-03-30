# 🖥️ Dual Boot: Windows 11 + Arch Linux (Guía Paso a Paso)

## 📌 1. Configuración Previa en Windows

### **Deshabilitar Inicio Rápido de Windows**
1. Presiona `Win + R`, escribe `powercfg.cpl` y presiona `Enter`  
2. Haz clic en **"Elegir el comportamiento de los botones de encendido"**  
3. Haz clic en **"Cambiar la configuración actualmente no disponible"**  
4. Desmarca **"Activar inicio rápido"**  
5. Guarda los cambios  

### **Verificar Modo UEFI**
```bash
msinfo32
```
- Debe decir **UEFI** en "Modo de BIOS".  

### **Desactivar BitLocker (Si está activado)**
```bash
Panel de control > Cifrado de unidad BitLocker
```
- Desactívalo si está activo en el disco principal.  

### **Liberar Espacio para Arch Linux**
1. Abre `Administrador de discos` (`diskmgmt.msc`)  
2. Encuentra tu unidad con Windows (`C:`)  
3. Haz clic derecho y selecciona **"Reducir volumen"**  
4. Libera al menos **50GB**  
5. No formatees el espacio libre.  

---

## 💿 2. Bootear desde el USB con Arch Linux

1. Inserta el USB con Arch Linux.  
2. Reinicia la PC y presiona `ESC` repetidamente para abrir el **menú de inicio de HP**.  
3. Selecciona **"F9 - Opciones de dispositivo de arranque"**.  
4. Elige el **USB UEFI**.  
5. Cuando cargue el menú de Arch Linux, selecciona **Boot Arch Linux**.  

---

## 🚀 3. Instalar Arch Linux

### **Conectar a Internet**
Si usas WiFi:  
```bash
iwctl
station wlan0 connect YOUR_WIFI_NAME
```

### **Verificar las Particiones Existentes**  
```bash
lsblk
```
- Muestra la estructura de discos y particiones.  

### **Crear Particiones para Arch Linux**
```bash
cfdisk /dev/nvme0n1
```
- Deja intactas las particiones de Windows.  
- Crea una partición root (`/`) en el espacio libre restante.  

### **Formatear Partición de Arch Linux**
```bash
mkfs.ext4 /dev/nvme0n1pX
```

### **Montar las Particiones**
```bash
mount /dev/nvme0n1pX /mnt
mkdir -p /mnt/boot/efi
mount /dev/nvme0n1p1 /mnt/boot/efi
```

---

## 📦 4. Instalar Arch Linux Base System  
```bash
pacstrap /mnt base linux linux-firmware nano
```

### **Generar fstab**
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

### **Ingresar al Sistema**
```bash
arch-chroot /mnt
```

### **Configurar Hora y Zona Horaria**
```bash
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
hwclock --systohc
```

### **Configurar Idioma del Sistema**
```bash
nano /etc/locale.gen
locale-gen
echo "LANG=en_US.UTF-8" > /etc/locale.conf
```

### **Configurar el Hostname**
```bash
echo "myarch" > /etc/hostname
```

### **Configurar Contraseña Root**
```bash
passwd
```

---

## 🔌 5. Instalar el Gestor de Arranque (GRUB) con Dual Boot

### **Instalar GRUB y Herramientas EFI**
```bash
pacman -S grub efibootmgr os-prober
```

### **Habilitar Detección de Windows**
```bash
nano /etc/default/grub
```
- Busca `GRUB_DISABLE_OS_PROBER=true` y cámbialo a `false`.  

### **Instalar GRUB en el Sistema**
```bash
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

---

## 🔄 6. Finalizar Instalación  
```bash
exit
umount -R /mnt
reboot
```

Si Windows no aparece en GRUB después del reinicio, ejecutar:  
```bash
sudo os-prober
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

---

## 🎯 7. Post-Instalación (Opcional, Recomendado)

### **Crear Usuario Normal**
```bash
useradd -m -G wheel -s /bin/bash myuser
passwd myuser
```

### **Habilitar sudo**
```bash
pacman -S sudo
EDITOR=nano visudo
```
- Descomenta:  
  ```
  %wheel ALL=(ALL) ALL
  ```

### **Habilitar WiFi**
```bash
pacman -S networkmanager
systemctl enable NetworkManager
```

### **Instalar un Entorno de Escritorio**
Para **GNOME**:  
```bash
pacman -S gnome gdm
systemctl enable gdm
```
Para **KDE Plasma**:  
```bash
pacman -S plasma kde-applications
systemctl enable sddm
```
---

