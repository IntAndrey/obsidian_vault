> It uses Docker and takes a lot of space, it will not fit into most MikroTik routers

It has [linux-kernel-module](https://github.com/amnezia-vpn/amneziawg-linux-kernel-module) fyi  
  
And awg tun interface can be linked to vanilla wireguard:

> Jc = 1 ≤ Jc ≤ 128; recommended range is from 3 to 10 inclusive  
> Jmin = Jmin < Jmax; recommended value is 50  
> Jmax = Jmin < Jmax ≤ 1280; recommended value is 1000  
> S1 = 0  
> S2 = 0  
> H1 = 1  
> H2 = 2  
> H3 = 3  
> H4 = 4