# WP-Migration-Using_Terraform
<h3>Wp Site</h3>
<p>Set up Wordpress with Lamp on both ec2 instnces and sudo passwd username</p>
<h3>File Transfer</h3>
<ul><h6>Run these command on both ec2 instances for permission</h6>
<li>sudo nano /etc/ssh/sshd_config</li>
<li>Set PasswordAuthentication=y, ChallengeResponseAuthentication=n, PermitRootLogin no,
PubkeyAuthentication yes, #GSSAPIAuthentication yes,
#GSSAPICleanupCredentials no, UsePAM yes</li>
<li>chmod 0700 /home/[your-username]</li>
<li>chmod 0700 /home/your_home/.ssh</li>
<li>chmod 0600 /home/[username]/.ssh/authorized_keys</li>
<li>systemctl restart sshd</li>
<li>ssh target Ip</li>
</ul>
<h6>File Transfer</h6>
<ul>
<li>$ scp -i ec2_instance_1.pem ec2_instance_2.pem ubuntu@ec2_1_inst_IP:~
</li>
<li>ssh -i ec2_instance_1.pem ubuntu@ec2_inst_1</li>
<li>scp -i ec2_instance_2.pem file.zip ubuntu@ec2_inst_2:~</li>
</ul>
<h3>WordPress Database Setup</h3>
<h6>Instance 01</h6>
<ul><li>cd  /var/www/</li><li>
tar zcf ~/wordpress.tar.gz wordpress/</li><li>cd ~/</li><li>
sudo mysqldump --add-drop-table -u root wordpressDB > wordpressDB.sql</li></ul>
<h6>Instance 02</h6>
<ul><li>sudo mysql -uroot -e "drop database wordpressDB;"</li><li>
sudo rm -fR /var/www/wordpress</li><li>sudo systemctl reload apache2
</li>
<li>sudo mysql -uroot -e "create database wordpressDB;"</li>
<li>sudo mysql -uroot -e "CREATE USER 'wordpressUser'@'127.0.0.1' IDENTIFIED BY 'wpUserP@ss4wpDB';"</li>
<li>sudo mysql -uroot -e "GRANT ALL PRIVILEGES ON wordpressDB.* TO 'wordpressUser'@'127.0.0.1';"</li>
<li>sudo mysql -uroot -e "flush privileges;"</li>
<li>sudo mysql -uroot wordpressDB < ~/wordpressDB.sql</li>

<li>sudo tar zxf ~/wordpress.tar.gz -C /var/www</li>

<li>sudo systemctl reload apache2

</li>
<li>


</ul>
