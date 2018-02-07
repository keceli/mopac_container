From: ubuntu:latest
Bootstrap: docker
%help
You either need to have a mopac_license.txt file in your home directory,
or you need to edit the recipe with your own license key.
%setup
echo "Home directory during setup" $HOME
echo "Creating directory:"  ${SINGULARITY_ROOTFS}/opt/mopac
mkdir -p ${SINGULARITY_ROOTFS}/opt/mopac
if [ -f  $HOME/mopac_license.txt ] ; then
  echo "Copying license file at" $HOME
  cp -p $HOME/mopac_license.txt ${SINGULARITY_ROOTFS}/opt/mopac
fi
if [ -f  mopac_license.txt ] ; then
  echo "Copying license file at" $PWD "to" ${SINGULARITY_ROOTFS}/opt/mopac
  cp -p $HOME/mopac_license.txt ${SINGULARITY_ROOTFS}/opt/mopac
fi
%post
echo "************************************************************"
echo "Installling required components"
echo "************************************************************" 
  apt-get -y install wget unzip
echo "************************************************************"
echo "Installling MOPAC"
echo "************************************************************"    
  echo "Home directory during post" $HOME
  mkdir -p /opt/mopac
  chmod 777 /opt/mopac
  cd /opt/mopac
  wget http://openmopac.net/MOPAC2016_for_Linux_64_bit.zip
  unzip MOPAC2016_for_Linux_64_bit.zip
  export LD_LIBRARY_PATH=/opt/mopac
  chmod +x /opt/mopac/MOPAC2016.exe
  # Type your MOPAC license key, and uncomment the following line
  #./MOPAC2016.exe $MOPAC_LICENSE_KEY
  if [ -f  ./mopac_license.txt ] ; then
    echo -ne '\n' "Yes"  | ./MOPAC2016.exe $(cat mopac_license.txt)
  fi
%environment
  LD_LIBRARY_PATH=/opt/mopac
  export LD_LIBRARY_PATH
%runscript
  echo "Running mopac with input file $1"
  exec /opt/mopac/MOPAC2016.exe "$1"
