From: ubuntu:latest
Bootstrap: docker

%post
echo "************************************************************"
echo "Installling required components"
echo "************************************************************" 
  apt-get -y install wget unzip
echo "************************************************************"
echo "Installling MOPAC"
echo "************************************************************"    
  mkdir -p /opt/mopac
  sudo chmod 777 /opt/mopac
  cd /opt/mopac
  wget http://openmopac.net/MOPAC2016_for_Linux_64_bit.zip
  unzip MOPAC2016_for_Linux_64_bit.zip
  export LD_LIBRARY_PATH=/opt/mopac
  chmod u+x /opt/mopac/MOPAC2016.exe
  echo -ne '\n' "Yes"  | ./MOPAC2016.exe $(cat ~/mopac_license.txt)
%environment
  LD_LIBRARY_PATH=/opt/mopac
  export LD_LIBRARY_PATH
%runscript
  echo "Running mopac with input file $*"
	exec /opt/mopac/MOPAC2016.exe "$@"
