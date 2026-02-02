docker-compose.yml
services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    user: root
    volumes:
      - ./prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/var/lib/prometheus
    ports:
      - "9090:9090"
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/var/lib/prometheus'
      - '--storage.tsdb.retention.time=90d'
    restart: always

  mktxp:
    container_name: mktxp
    image: ghcr.io/akpw/mktxp:latest
    user: root
    volumes:
      - ./mktxp:/root/mktxp:rw
    ports:
      - "49090:49090"
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    volumes:
      - ./grafana/grafana:/etc/grafana/provisioning
      - grafana_data:/var/lib/grafana1
    environment:
      - GF_SECURITY_ADMIN_USER=insiMonitoring
      - GF_SECURITY_ADMIN_PASSWORD=warnever1
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
    restart: always

volumes:
  prometheus_data:
  grafana_data:

mktxp conf

    [Insi RB5009]
    hostname = 192.168.50.1    # IP роутера который будем мониторит

[Insi RB2011]
    hostname = 192.168.50.13

[Insi HapAc2]
    hostname = 192.168.50.19

[Suv RB1100]
    hostname = 192.168.88.1

[Tank HapAc2]
    hostname = 192.168.101.1

[Depo2 Hex]
    hostname = 192.168.80.1

[Mshk HexS]
    hostname = 192.168.90.1

[Gam Hex]
    hostname = 192.168.85.1

[Suv Bridge Master]
    hostname = 192.168.88.252

[Suv Bridge Slave]
    hostname = 192.168.88.238

[Top Hex]
    hostname = 192.168.92.1

[Bikin WL-mas]
    hostname = 87.225.109.157

[Per Hex]
    hostname = 192.168.84.1

[Hex Kontur]
    hostname = 192.168.81.1
    route = False
    routing_stats = False

[Nik Hex]
    hostname = 192.168.94.1
    custom_labels = dc:Nikolaevka, rack=hex, service:prod

[default]

    enabled = True    # turns metrics collection for this RouterOS device on / off
    hostname = localhost    # RouterOS IP address
    port = 8729    # RouterOS IP Port

    username = InsiMonitoring    # RouterOS user, needs to have 'read' and 'api' permissions
    password = J5Y8W2LciSPqijFv3erTU

    use_ssl = True    # enables connection via API-SSL servis
    no_ssl_certificate = True    # enables API_SSL connect without router SSL certificate
    ssl_certificate_verify = False    # turns SSL certificate verification on / off
    plaintext_login = True    # for legacy RouterOS versions below 6.43 use False

    installed_packages = True    # Installed packages
    dhcp = True    # DHCP general metrics
    dhcp_lease = True    # DHCP lease metrics

    connections = True    # IP connections metrics
    connection_stats = True    # Open IP connections metrics

    interface = True    # Interfaces traffic metrics

    route = False    # IPv4 Routes metrics
    pool = True    # IPv4 Pool metrics
    firewall = True    # IPv4 Firewall rules traffic metrics
    neighbor = True    # IPv4 Reachable Neighbors
    dns = True    # DNS stats

    ipv6_route = False    # IPv6 Routes metrics
    ipv6_pool = False    # IPv6 Pool metrics
    ipv6_firewall = False    # IPv6 Firewall rules traffic metrics
    ipv6_neighbor = False    # IPv6 Reachable Neighbors

    poe = True    # POE metrics
    monitor = True    # Interface monitor metrics
    netwatch = True    # Netwatch metrics
    public_ip = True    # Public IP metrics
    wireless = True    # WLAN general metrics
    wireless_clients = True    # WLAN clients metrics
    capsman = False    # CAPsMAN general metrics
    capsman_clients = False    # CAPsMAN clients metrics

    eoip = False    # EoIP status metrics
    gre = True    # GRE status metrics
    ipip = False    # IPIP status metrics
    lte = False    # LTE signal and status metrics (requires additional 'test' permission policy on RouterOS v6)
    ipsec = True    # IPSec active peer metrics
    switch_port = True    # Switch Port metrics

    kid_control_assigned = True    # Allow Kid Control metrics for connected devices with assigned users
    kid_control_dynamic = True    # Allow Kid Control metrics for all connected devices, including those without assigned user

    user = True    # Active Users metrics
    queue = True    # Queues metrics

    bgp = True    # BGP sessions metrics
    routing_stats = True    # Routing process stats
    certificate = True    # Certificates metrics

    remote_dhcp_entry = None    # An MKTXP entry to provide for remote DHCP info / resolution
    remote_capsman_entry = None    # An MKTXP entry to provide for remote capsman info
    check_for_updates = True    # check for available ROS updates
    interface_name_format = name

# The section below contains the latest default parameters introduced by MKTXP
# For organizational purposes, you can move these parameters to the [default] section
[new_default_parameters]
    w60g = False
    bfd = False
    ssl_check_hostname = True
    container = False
    health = True
    credentials_file = ""
    ssl_ca_file = ""
    address_list = None
    ipv6_address_list = None
    custom_labels = None

#InsiConfigsNotes