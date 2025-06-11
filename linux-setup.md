sudo apt update
sudo apt install mono-complete
sudo dpkg --configure -a
sudo apt update
sudo apt upgrade -y
sudo apt install git
git clone https://github.com/opensim/opensim.git
git clone https://github.com/diva/d2.git
sudo apt update
sudo apt install nant
cd ~/robustos/opensim
sh runprebuild.sh
dotnet build OpenSim.sln
dotnet build OpenSim.sln --configuration Release
cp ~/robustos/d2/Configs/OpenSim.ini ~/robustos/opensim/bin/OpenSim.ini
cp ~/robustos/d2/Configs/RegionConfig.ini.example ~/robustos/opensim/Regions/Regions.ini
cp ~/robustos/d2/Configs/MyWorld.ini.example ~/robustos/opensim/bin/MyWorld.ini

nano ~/robustos/opensim/bin/OpenSim.ini
add before const
[DatabaseService]
Include-Storage = "config-include/storage/SQLiteStandalone.ini"

mkdir -p ~/robustos/opensim/config-include/storage
nano ~/robustos/opensim/config-include/storage/SQLiteStandalone.ini

[SQLiteDatabase]
Filename = "OpenSim.sqlite"
Version = 3

chmod +x opensim.sh
./opensim.sh
