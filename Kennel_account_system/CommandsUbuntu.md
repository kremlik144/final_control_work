## Task-1
mkdir Kennel    
cd ~/Kennel    
cat > home_animals    
cat > pack_animals    
cat home_animals pack_animals > animals    
cat animals    
mv animals mans_friends    
ls   

## Task-2
cd ..    
mkdir Kennel-2   
cd Kennel   
mv mans_friends ~/Kennel-2  
cd ..  
cd Kennel-2  
ls -lm  

## Task-3
sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.23-1_all.deb    
sudo dpkg -i mysql-apt-config_0.8.23-1_all.deb    
sudo apt-get update    
sudo apt-get install mysql-server    

## Task-4
sudo wget https://download.docker.com/linux/ubuntu/dists/jammy/pool/stable/amd64/docker-ce-cli_20.10.13~3-0~ubuntu-jammy_amd64.deb    
sudo dpkg -i docker-ce-cli_20.10.13~3-0~ubuntu-jammy_amd64.deb    
sudo dpkg -r docker-ce-cli    
