# grib2-dps
Como transformar gfs (grib2) em dp (brams) do início [30/09/2019]

Sugestão de download do gfs: https://nomads.ncep.noaa.gov/pub/data/nccf/com/gfs/prod/
Descompactar arquivos.tar.xz: tar xvzf arquivos.tar.xz 

Após descompatar, trÊs arquivos surgirão: 
wgrib.tgz, 
g2ctl.pl e 
geraDP.tgz. 


1- Instalar wgrib2
Descompactar: tar xvzf wgrib2.tgz
Mover para /usr/local: mv grib2 /usr/local
Para ambiente em bash: 

export CC=gcc
export FC=gfortran
make

2- Instalar g2ctl

Modificar onde houver $wgrib2='wgrib2'; para $wgrib2='/usr/local/grib2/wgrib2/wgrib2';

Alterar as permissoes do arquivo: sudo chmod 755 g2ctl.pl

Copiar p/ o bin de todos os usuários: sudo cp g2ctl.pl /usr/bin

********************** Gerando ctl de gfs.grib2 ********************** 

g2ctl -0 gfs.t00z.pgrb2.0p25.f000 > gfs.t00z.pgrb2.0p25.f000.ctl

Para utilizar no geraDP:

É preciso gerar um idx pelo gribmap

No terminal: 
gribmap -iv gfs.t00z.pgrb2.0p25.f000.ctl

3 - Instalar geraDP

Na pasta dprep do BRAMS, descompactar: 

tar xvzf geraDP.tgz

Copiar os arquivos gfs (grib2, ctl e idx) para esta mesma pasta (dprep)

Modificações obrigatórias do geraDP.ini*:

ctl_file_name=o nome do seu ctl aqui
wind_u_varname='UGRDprs'
wind_v_varname='VGRDprs'
temperature_varname='TMPprs'
geo_varname='HGTprs'
ur_varname='RHprs' 
                                       
* para arquivos gfs nomads. Nomes definidos nos arquivos ctl, gerados no item 2.  

EXTRA: 
Modificar o caminho da opção IAPR no RAMSIN, para rodada no modelo BRAMS. 
