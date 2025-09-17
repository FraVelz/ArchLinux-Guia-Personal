¡Perfecto, gracias por aclararlo! 🧠
Entonces lo que estás viendo **antes de SDDM** (antes de la pantalla de login) es lo siguiente:

---

## 🧩 Etapas de arranque antes del login

Cuando prendes el PC, el flujo es más o menos así:

```
Encendido → BIOS/UEFI → GRUB → Kernel → Plymouth → SDDM → Hyprland
```

Las partes importantes que puedes **personalizar visualmente** son:

---

## ⚙️ 1. GRUB (gestor de arranque)

* Es el menú que aparece **apenas enciendes**, donde eliges el sistema operativo.
* Normalmente es texto negro con letras blancas.

🔧 Para personalizarlo:

```bash
sudo nano /etc/default/grub
```

Busca la línea:

```
GRUB_THEME=
```

Y pon la ruta a un tema que hayas instalado, por ejemplo:

```
GRUB_THEME="/boot/grub/themes/mi-tema/theme.txt"
```

Luego aplica cambios:

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

---

## 🌌 2. Plymouth (pantalla de carga)

* Se muestra **después de GRUB y antes de SDDM**.
* Es la típica **pantalla de carga con logo o animación** mientras arranca el sistema.
* Aquí es donde aparece ese "tema de carga" que mencionas.

🔧 Instalación:

```bash
sudo pacman -S plymouth
```

🔧 Activarlo (muy importante):

```bash
sudo nano /etc/mkinitcpio.conf
```

En la línea `HOOKS=`, pon `plymouth` justo después de `base` y antes de `udev`, por ejemplo:

```
HOOKS=(base plymouth udev ... )
```

Regenera la imagen initramfs:

```bash
sudo mkinitcpio -P
```

🔧 Configurar tema:

Ver los temas disponibles:

```bash
sudo plymouth-set-default-theme -l
```

Elegir uno:

```bash
sudo plymouth-set-default-theme -R spinner
```

(O reemplaza `spinner` por el nombre del tema que elijas.)

---

## 🖥️ 3. SDDM (pantalla de login)

Después de Plymouth aparece SDDM, que ya vimos cómo configurar en los pasos anteriores.

---

## 📌 Resumen

* **GRUB** → pantalla inicial con menú del sistema.
* **Plymouth** → pantalla de carga animada mientras el sistema inicia.
* **SDDM** → pantalla de inicio de sesión gráfica.

---

Si quieres, puedo darte **un tema bonito y moderno de Plymouth** para que tu arranque se vea profesional.
¿Quieres que lo haga?

