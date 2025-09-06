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

**Asignación de PCs a puertos de acceso:**
- `cliente01`: PC-A1 → Fa0/11, PC-M1 → Fa0/12, PC-V1 → Fa0/13  
- `cliente02`: PC-A2 → Fa0/11, PC-M2 → Fa0/12, PC-V2 → Fa0/13

*Inserta aquí una captura adicional si lo deseas:*  
![Detalle de puertos](<-- pega_la_URL_aquí --> "Captura: Puertos de acceso")

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

*Captura de configuración IP en una PC:*  
![IP en PC](<-- pega_la_URL_aquí --> "Captura: IP de PC")

---

## 3. Scripts de configuración (copiar/pegar)

> Nota: Los **2960** no requieren `switchport trunk encapsulation`.  
> Asegúrate de usar **VTP v2** en todos.

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
