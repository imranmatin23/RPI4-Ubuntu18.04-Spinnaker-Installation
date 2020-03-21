# Ubuntu Server 18.04 and Spinnaker SDK Installation on RPI4 Steps

This is a guide to installing Ubuntu Server 18.04 and Spinnaker SDK onto your RPI4. It is meant to support
image acquisition.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them. These downloads can be either on your local computer
and then use SCP to transfer them onto the remote computer, or can be downloaded straight onto the remote computer.

1. Download 64-bit Ubuntu Server 18.04.4 LTS from this [link](https://ubuntu.com/download/raspberry-pi/thank-you?version=18.04.4&architecture=arm64+raspi3).
2. Download the Archiconda installation script from this [link](https://github.com/Archiconda/build-tools/releases).
3. Download the Spinnaker for ARM64 package from this [link](https://flir.app.boxcn.net/v/SpinnakerSDK/file/546291925389).
4. Download the Python wrapper for Spinnaker for ARM64 package from this [link](https://flir.app.boxcn.net/v/SpinnakerSDK/file/546280393001).
5. Install BalenaEtcher from this [link](https://www.balena.io/etcher/).


### Installing Ubuntu

A step by step guide that tell you how to install Ubuntu.

1. Unzip the compressed Ubuntu Server 18.04 file.
```
unxz --keep ubuntu-18.04.4-preinstalled-server-arm64+raspi3.img.xz
```
2. Burn the .img onto the MicroSD using BalenaEtcher.
3. Insert the MicroSD into the RPI4.
4. Power on the RPI4.
5. Login using default login:
    - Username: ubuntu
    - Password: ubuntu
6. Set your new password.
7. Check SSH is running.
```
sudo systemctl status ssh
ip address
```
8. Login on your remote computer.
```
ssh -X ubuntu@[IP_ADDRESS]
```
10. Check if system is running other apt update processes.
```
ps aux | grep -i apt
```
11. Update and upgrade the system.
```
sudo apt update -y && sudo apt upgrade -y
```
12. Install Ubuntu Desktop (Optional)
```
sudo apt-get install ubuntu-desktop
reboot
```


### Installing Spinnaker

A step by step guide that tell you how to install Spinnaker.

1. Download this repository.
```
mkdir ~/Desktop
cd ~/Desktop
git clone https://github.com/imranmatin23/MPL-Research.git
mkdir ~/Downloads
cd ~/Downloads
scp [LOCAL_PATH]/Archiconda3-0.2.3-Linux-aarch64.sh ubuntu@[IP_ADRESS]:/home/ubuntu/Downloads 
```
2. On line 2 of the Archiconda script, replace “#” with a blank line.
3. Install Archiconda and follow onscreen instructions. Exit out of SSH session when complete. Activate Archiconda.
```
sh Archiconda3-0.2.3-Linux-aarch64.sh
exit
ssh -X ubuntu@[IP_ADDRESS]
echo "conda activate" >> ~/.bashrc
. ~/.bashrc
conda activate
```
4. Create Spinnaker Python environment.
```
sh create_spinnaker_env.sh
conda activate
conda activate spinnaker_py37
```
5. Install Spinnaker and follow onscreen instructions.
```
scp [LOCAL_PATH]/spinnaker-1.27.0.48-Ubuntu18.04-arm64-pkg.tar.gz ubuntu@[IP_ADRESS]:/home/ubuntu/Downloads
scp [LOCAL_PATH]/spinnaker_python-1.27.0.48-Ubuntu18.04-cp37-cp37m-linux_aarch64.tar.gz ubuntu@[IP_ADRESS]:/home/ubuntu/Downloads
sh install_spinnaker.sh
```
6. Begin acquiring images.
```
sh spinnaker_acquisition.sh
```


End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc

