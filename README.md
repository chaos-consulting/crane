# Crane

A buttler (aka home automation) system for C2IS.
Named after Alfred Thaddeus Crane Pennyworth.

## ansible scripts

Ausgehend von einer frischen [Raspbian-Installation](…) können die Scripte genutzt werden, um die das komplette Setup
zu replizieren.

Derzeit existieren drei Playbooks. `init.yml`, `main.yml` und  `upgrade.yml`.
Ersteres legt eine Menge an (Admin-)Usern auf dem System an und konfiguriert die wesentlichsten Dinge.
Per SSH meldet man sich als User `pi` und einem Passwort an.
Danach können die konfigurierten Admin-User das `main.yml` Playbook nutzen, um alles Weitere einzurichten.

Systemupdates können mit `upgrade.yml` durchgeführt werden.

### HowTo `init.yml`

```bash
ansible-playbook -i hosts init.yml -k
```

Durch den Parameter `-k` fragt ansible nach dem Passwort für den Nutzer `pi`.
Dieses Playbook wird vermutlich selten ausgeführt.

### HowTo `main.yml`

```bash
ansible-playbook -i hosts main.yml --vault-password-file=.vaultpass.txt
```

Installiert die Offline-Version von openHAB2 inkl. einiger Tools und der Konfiguration für die Installation
in den Räumen von Chaos-Consulting.

## HowTo `upgrade.yml`

```bash
ansible-playbook -i hosts upgrade.yml
```

Aktualisiert das System und rebootet es, wenn die Updates dies verlangen.

