# Manual Tecnico de Condiguracioces de Red
## Tabla de Direcciones IP
	
| Dispositivo       | Dirección IP   |
|-------------------|----------------|
| PC0               | 192.168.98.1   |
| PC1               | 192.168.98.2   |
| PC2               | 192.168.98.3   |
| PC3               | 192.168.98.4   |
| PC4               | 192.168.98.5   |
| PC5               | 192.168.98.6   |
| PC6               | 192.168.98.7   |
| PC7               | 192.168.98.8   |
| PC8               | 192.168.98.9   |
| PC9               | 192.168.98.10  |
| PC10              | 192.168.98.11  |
| PC11              | 192.168.98.12  |
| PC12              | 192.168.98.13  |
| PC13              | 192.168.98.14  |
| PC14              | 192.168.98.15  |
| PC15              | 192.168.98.16  |
| PC16              | 192.168.98.17  |
| PC17              | 192.168.98.18  |
| PC18              | 192.168.98.19  |
| PC19              | 192.168.98.20  |
| PC20              | 192.168.98.21  |
| PC21              | 192.168.98.22  |
| PC22              | 192.168.98.23  |
| PC23              | 192.168.98.24  |
| PC24              | 192.168.98.25  |
| PC25              | 192.168.98.26  |
| PC26              | 192.168.98.27  |
| PC27              | 192.168.98.28  |
| PC28              | 192.168.98.29  |
| PC29              | 192.168.98.30  |
| PC30              | 192.168.98.31  |
| PC31              | 192.168.98.32  |
| PC32              | 192.168.98.33  |
| PC33              | 192.168.98.34  |
| PC34              | 192.168.98.35  |
| PC35              | 192.168.98.36  |
| PC36              | 192.168.98.37  |
| PC37              | 192.168.98.38  |
| Laptop0           | 192.168.98.39  |
| Laptop1           | 192.168.98.40  |
| Laptop2           | 192.168.98.41  |
| Laptop3           | 192.168.98.42  |
| Laptop4           | 192.168.98.43  |
| Laptop5           | 192.168.98.44  |
| Laptop6           | 192.168.98.45  |
| Laptop7           | 192.168.98.46  |
| Laptop8           | 192.168.98.47  |
| Laptop9           | 192.168.98.48  |
| Laptop10          | 192.168.98.49  |
| Laptop11          | 192.168.98.50  |
| Laptop12          | 192.168.98.51  |
| Laptop13          | 192.168.98.52  |
| Laptop14          | 192.168.98.53  |
| Laptop15          | 192.168.98.54  |
| Laptop16          | 192.168.98.55  |
| Laptop17          | 192.168.98.56  |
| Server0           | 192.168.98.57  |
| Server1           | 192.168.98.58  |
| Server2           | 192.168.98.59  |

# Configuración básica de hostname y contraseñas en un switch

## 1) Modo privilegiado y configuración global
Switch> enable
Switch# configure terminal

## 2) Cambiar el nombre del equipo (hostname)
Switch(config)# hostname SW_NOMBRE

## 3) Contraseña del modo privilegiado (enable)
# Opción recomendada (encriptada):
SW_NOMBRE(config)# enable secret 202010298
# (Si por algún motivo te piden la simple)
# SW_NOMBRE(config)# enable password 202010298

## 4) Contraseña para la CONSOLA (line console 0)
SW_NOMBRE(config)# line console 0
SW_NOMBRE(config-line)# password 202010298
SW_NOMBRE(config-line)# login
SW_NOMBRE(config-line)# exit

## 5) Salir y guardar
SW_NOMBRE(config)# end
SW_NOMBRE# write


# Capturas de VPC

![VPC1](https://github.com/seb4sr/Redes1_2S_2025_202010298/blob/main/Images/vpc1.png)
![VPC2](URL_DE_LA_IMAGEN)
![VPC3](URL_DE_LA_IMAGEN)
![VPC4](URL_DE_LA_IMAGEN)
![VPC5](URL_DE_LA_IMAGEN)
![VPC6](URL_DE_LA_IMAGEN)
![VPC7](URL_DE_LA_IMAGEN)
![VPC8](URL_DE_LA_IMAGEN)
![VPC9](URL_DE_LA_IMAGEN)
![VPC10](URL_DE_LA_IMAGEN)


# Capturas de paquetes ARP y ICMP

![ARP](URL_DE_LA_IMAGEN)
![ICMP](URL_DE_LA_IMAGEN)


