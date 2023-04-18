# fedora-config
In this repository I will put in all the steps I follow every time I install fedora.
The steps below are taken from a youtube video (link below), I am just putting all the commands together in one place.

<a href="https://www.youtube.com/watch?v=RrRpXs2pkzg&t=1s&ab_channel=TechHut">TechHut's youtube video: 7 things you MUST DO after installing fedora</a>


<h3>DNF Package Manager configuration</h3>
<p>Open the configuration file located at <strong>/etc/dnf/dnf.conf</strong> with an editor, we will need sudo privileges.</p>

```
sudo nano /etc/dnf/dnf.conf
```

<p>Here is what I add:</p>
<pre>
  fastestmirror=True                
  max_parallel_downloads=4        
  defaultyes=True                
  keepcache=True                
</pre>

<ul>
  <li>The amount of parallel downloads depends on network speeds, I stick to 4 but it can be anything.</li>
  <li>defaultyes makes it so that when installing packages, if you press ENTER, it will take it as a Yes (default is No in fedora)</li>
</ul>

<a href="https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbUFDcVRabnlNcWRWYlRkWWFyQjFIUlRvcHgyUXxBQ3Jtc0tsaERkb2tRUEVtN1pSR0hXS0NPRkpITDRFenlNLWh5ZUNNQUJZVG9tZk1DSTF4WGVXUXpOZUpGXzhtNlJta21NY2lIVkpvcU4xUGhUWk1IanZkdkhiTFBlc2tpYnpKQWF3TmdqM0FMQnlBVmE0aTNJVQ&q=https%3A%2F%2Fdnf.readthedocs.io%2Fen%2Flatest%2Fconf_ref.html&v=RrRpXs2pkzg">Read DNF Documentation</a>
<p>For clearing the cache use (either one of these):</p>

```
sudo dnf clean dbcache
```

```
sudo dnf clean all
```

<h3>Update the system</h3>

```
sudo dnf update -y
```

<h3>Enable RPM Fusion (repository with proprietary software)</h3>
<p><a href="https://rpmfusion.org/Configuration">Configure RPM Fusion</a></p>

```
sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

<p>The following command is used to install the AppStream metadata (used for installing packages via GUI)</p>

```
sudo dnf groupupdate core
```

<h3>Add Flatpak</h3>
<p>Fedora has built-in support for flatpak, but it is stripped down. We want to add the flathub.com repository.</p>
<p><a href="https://flatpak.org/setup/Fedora">Flatpak setup</p>

```
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

<h3>Installing media codecs</h3>
<p>Fedora does not include much when it comes to media codecs, so we need to add them.</p>

```
sudo dnf groupupdate multimedia --setop="install_weak_deps=False" --exclude=PackageKit-gstreamer-plugin
sudo dnf groupupdate sound-and-video
```

<h3>Change Hostname</h3>

```
sudo hostnamectl set-hostname "New_Custom_Name"
```
