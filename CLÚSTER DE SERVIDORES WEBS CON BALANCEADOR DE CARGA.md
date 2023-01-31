## Datos de usuario
sudo apt update

sudo apt install apache2

### HTML
```
<html>
	<head>
		<title>Mi página de ejemplo</title>
	</head>
	<body>
	Aquí va el contenido
	</body>
</html>
```

### MySQL
sudo apt install mysql-server

## Balanceador de carga
sudo apt update

sudo apt install apache2

sudo a2enmod proxy

sudo a2enmod proxy_http

sudo a2enmod proxy_ajp

sudo a2enmod rewrite

sudo a2enmod deflate

sudo a2enmod headers

sudo a2enmod proxy_balancer

sudo a2enmod proxy_connect

sudo a2enmod proxy_html

sudo a2enmod lbmethod_byrequests

sudo systemctl restart apache2


### Proxy inverso
sudo nano /etc/apache2/sites-enabled/000-default.conf
```
<Proxy balancer://mycluster>
        # Server 1
        BalancerMember http://IP-HTTP-SERVER-1
        # Server 2
        BalancerMember http://IP-HTTP-SERVER-2
</Proxy>

   ProxyPass / balancer://mycluster/


<Location /balancer-manager>
       SetHandler balancer-manager
       Order Deny,Allow
       Allow from all
</Location>

ProxyPassReverse / balancer://mycluster/
```
