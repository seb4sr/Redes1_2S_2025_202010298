    # Tarea #3 — VLANs y VTP (Packet Tracer)
**Curso:** Redes de Computadoras 1  
**Alumno:** Sergio Sandoval — Carné **202010298**  


> **Convenciones con el carné 202010298:**  
> X = **8** ⇒ VLAN**18**=ADMON, VLAN**28**=MERCA, VLAN**38**=VENTAS.  
> VTP domain/password: **202010298**

---

## 1. Topología

**Diagrama de la topología (enlace entre switches y puertos):**  
![Topología general](https://github.com/seb4sr/Redes1_2S_2025_202010298/blob/main/T3/images/topo.png "Captura: Topología")

**Detalle de enlaces entre switches (FastEthernet):**
- `servidor` **Fa0/1** ↔ `transparente` **Fa0/1**
- `transparente` **Fa0/2** ↔ `cliente01` **Fa0/1**
- `transparente` **Fa0/3** ↔ `cliente02` **Fa0/1**
- `cliente01` **Fa0/2** ↔ `cliente02` **Fa0/2**

---

## 2. Direccionamiento IP de las PCs

Todas /24 (sin gateway). Red de ejemplo: **192.158.100.0/24**.

| PC  | Switch/Port | VLAN | IP             | Máscara        |
|-----|-------------|------|----------------|----------------|
| A1  | cliente01/Fa0-11 | 18 (ADMON) | 192.158.100.11 | 255.255.255.0 |
| A2  | cliente02/Fa0-11 | 18 (ADMON) | 192.158.100.12 | 255.255.255.0 |
| M1  | cliente01/Fa0-12 | 28 (MERCA) | 192.158.100.21 | 255.255.255.0 |
| M2  | cliente02/Fa0-12 | 28 (MERCA) | 192.158.100.22 | 255.255.255.0 |
| V1  | cliente01/Fa0-13 | 38 (VENTAS)| 192.158.100.31 | 255.255.255.0 |
| V2  | cliente02/Fa0-13 | 38 (VENTAS)| 192.158.100.32 | 255.255.255.0 |

---

## 3. Scripts de configuración (copiar/pegar)


### 3.1 Switch `servidor` (VTP **server** + creación de VLANs)
```plaintext
enable
conf t
hostname servidor
vtp mode server
vtp version 2
vtp domain 202010298
vtp password 202010298

interface fa0/1
 switchport mode trunk
 switchport trunk allowed vlan 18,28,38
 no shutdown
exit

vlan 18
 name ADMON
vlan 28
 name MERCA
vlan 38
 name VENTAS
end
wr

### 3.2 Switch `transparente` (VTP **transparente** + creación de VLANs)
```plaintext
enable
conf t
hostname transparente
vtp mode transparent
vtp version 2
! (alineado por buena práctica)
vtp domain 202010298
vtp password 202010298

interface range fa0/1 - 3
 switchport mode trunk
 switchport trunk allowed vlan 18,28,38
 no shutdown
end
wr

### 3.3 Switch `cliente1` (VTP **cliente1** + creación de VLANs)
```plaintext
enable
conf t
hostname cliente01
vtp mode client
vtp version 2
vtp domain 202010298
vtp password 202010298

interface range fa0/1 - 2
 switchport mode trunk
 switchport trunk allowed vlan 18,28,38
 no shutdown
exit

interface fa0/11
 switchport mode access
 switchport access vlan 18
 spanning-tree portfast
 no shutdown
exit

interface fa0/12
 switchport mode access
 switchport access vlan 28
 spanning-tree portfast
 no shutdown
exit

interface fa0/13
 switchport mode access
 switchport access vlan 38
 spanning-tree portfast
 no shutdown
end
wr

### 3.4 Switch `cliente2` (VTP **cliente2** + creación de VLANs)
```plaintext
enable
conf t
hostname cliente02
vtp mode client
vtp version 2
vtp domain 202010298
vtp password 202010298

interface range fa0/1 - 2
 switchport mode trunk
 switchport trunk allowed vlan 18,28,38
 no shutdown
exit

interface fa0/11
 switchport mode access
 switchport access vlan 18
 spanning-tree portfast
 no shutdown
exit

interface fa0/12
 switchport mode access
 switchport access vlan 28
 spanning-tree portfast
 no shutdown
exit

interface fa0/13
 switchport mode access
 switchport access vlan 38
 spanning-tree portfast
 no shutdown
end
wr

## 4. Verificación


### 4.1 Estado de VTP
En cada switch
```plaintext
show vtp status
https://github.com/seb4sr/Redes1_2S_2025_202010298/blob/main/T3/images/server2.png
https://github.com/seb4sr/Redes1_2S_2025_202010298/blob/main/T3/images/trans2.png
https://github.com/seb4sr/Redes1_2S_2025_202010298/blob/main/T3/images/c12.png
https://github.com/seb4sr/Redes1_2S_2025_202010298/blob/main/T3/images/c22.png