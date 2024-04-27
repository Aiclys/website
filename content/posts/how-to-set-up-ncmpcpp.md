+++
title = 'How to set up mpd with mpc and ncmpcpp'
author = 'Nyrs'
tags = ["guides", "cli", "linux", "software", "minimalism"]
date = 2024-04-12T14:42:33+01:00
+++

## Intro
#### Why should you use mpd, mpc and ncmpcpp and what are they? Mpd is a minimalistic but powerful music client/daemon that is used as backend in a lot of different apps for playing music. Managing it without any frontend is nearly impossible, which is why it is often used in combination with mpc for control and ncmpcpp as frontend to do things like browsing music files, choosing the song, arranging playlists etc. NCurses Music Player Client Plus Plus, also called ncmpcpp, is a rewrite of ncmpc in C++ (hence the plus plus). It also added new features such as extended song formats, a local file system browser and many more. These three applications excel in their ability of being highly customizable and flexible while being extremely fast and lightweight which is why I and a lot of other people use it instead of services like Spotify.

&nbsp;
&nbsp;

## Installation
### Install on Arch Linux and it's many decendants:
#### Install the stable version through the official repos:
```
$ sudo pacman -S mpd ncmpcpp mpc
```
#### or the latest development version using the AUR:
```
$ paru -S mpd-git ncmpcpp-git mpc-git
	or
$ yay -S mpd-git ncmpcpp-git mpc-git
```

### Install on Debian and it's many decendants:
```
$ sudo apt-get install mpd ncmpcpp mpc
```

&nbsp;
&nbsp;

## Configuration
### mpd
#### Mpd recognizes multiple folders/files as configuration files. This means that you can place your configuration file in `/etc/mpd.conf`, `~/.config/mpd/mpd.conf`, `~/.mpdconf` or in `~/.mpd/mpd.conf`. I prefer `~/.mpd/mpd.conf` but you can change it to your preference. If your chosen directory doesn't exist yet, create it. After instaling mpd it will most likely be launched as a system service automatically, which I don't want. To run mpd as a user process you need to disable the mpd system service and launch mpd manually to start it:
```
$ sudo systemctl disable mpd.service
$ sudo systemctl disable mpd.socket
```
#### If you want to use it as a system service you need to execute the following commands to add mpd to your login and audio group:
```
$ sudo gpasswd -a mpd your_login_group
$ chmod 710 ~/
$ sudo gpasswd -a mpd audio
```
#### Now it's time to create the config file and add the following content to it:
```
 bind_to_address "127.0.0.1"
 #bind_to_address "~/.mpd/socket"
 music_directory "~/your_music_folder"
 playlist_directory "~/your_playlist_folder"   
 db_file      "~/.mpd/mpd.db"  
 log_file      "~/.mpd/mpd.log"  
 pid_file      "~/.mpd/mpd.pid"  
 state_file     "~/.mpd/mpdstate"  
 audio_output {  

     type  "pulse"  
     name  "pulse audio"
     device         "pulse" 
     mixer_type      "hardware" 
 }  

audio_output {
    type                    "fifo"
    name                    "my_fifo"
    path                    "/tmp/mpd.fifo"
    format                  "44100:16:2"
}
```
#### If you want to use alsa instead of pulseaudio, change the `audio_output` code block as follows:
```
audio_output {
        type            "alsa"
        name            "alsa for audio sound card"
        mixer_type      "software" 
}
```

### ncmpcpp
#### Here is my config file (the config file should be located in~/.ncmpcpp/config so create the folder if it isn't there already):
```
## Files ##
mpd_music_dir = "your_music_folder"  
ncmpcpp_directory  = ~/.ncmpcpp
mpd_host = "localhost"
mpd_port = "6600"  
mpd_connection_timeout = "5"  
mpd_crossfade_time = "3"  

## Playlist ##
playlist_disable_highlight_delay = "0"  
playlist_display_mode = "columns"  
playlist_show_remaining_time = "yes"

browser_display_mode = "columns"  
autocenter_mode = "yes"  
fancy_scrolling = "yes"  
follow_now_playing_lyrics = "yes"  
display_screens_numbers_on_start = "yes"  
ignore_leading_the = "yes"  
lyrics_database = "1"  
song_columns_list_format = "(10)[blue]{l} (30)[green]{a} (30)[magenta]{b} (50)[yellow]{t}"  
colors_enabled = "yes"  
main_window_color = "white"  
main_window_highlight_color =  "blue"
header_window_color = "cyan"  
volume_color = "red"  
progressbar_color = "white"  
statusbar_color = "white"  
active_column_color = "cyan"  
active_window_border = "blue"

alternative_header_first_line_format = "$0$aqqu$/a {$7%a - $9}{$5%t$9}|{$8%f$9} $0$atqq$/a$9"
alternative_header_second_line_format = "{{$6%b$9}{ [$6%y$9]}}|{%D}"
song_list_format = "{$3%n │ $9}{$7%a - $9}{$5%t$9}|{$8%f$9}$R{$6 │ %b$9}{$3 │ %l$9}"
user_interface = "alternative"
#user_interface = "classic"
default_place_to_search_in = "database"

## Visualizer ##
visualizer_fifo_path = "/tmp/mpd.fifo"
visualizer_output_name = "my_fifo"
visualizer_sync_interval = "12"
visualizer_type = "wave" (spectrum/wave)
#visualizer_type = "spectrum" (spectrum/wave)
visualizer_in_stereo = "yes"
visualizer_look = "●┃"

## Navigation ##
cyclic_scrolling = "yes"
header_text_scrolling = "yes"
jump_to_now_playing_song_at_start = "yes"
lines_scrolled = "2"

## Other ##
system_encoding = "utf-8"
regular_expressions = "extended"

## Selected tracks ##
selected_item_prefix = "* "
discard_colors_if_item_is_selected = "no"

## Seeking ##
incremental_seeking = "yes"
seek_time = "1"

## Visivility ##
header_visibility = "yes"
statusbar_visibility = "yes"
titles_visibility = "yes"
progressbar_look =  "->_"
progressbar_boldness = "yes"
progressbar_elapsed_color = "white"
now_playing_prefix = ">> "
song_status_format = " $2%a $4⟫$3⟫ $8%t $4⟫$3⟫ $5%b "
autocenter_mode = "yes"
centered_cursor = "yes"

## Misc ##
display_bitrate = "yes"
# enable_window_title = "no"
follow_now_playing_lyrics = "yes"
ignore_leading_the = "yes"
empty_tag_marker = ""
```
#### To get the full example config file view the content in this file: `/usr/share/doc/ncmpcpp/config` and copy it over to your config folder if needed. There are near endless configuration possibilities, which is why I won't go every one of them here but you want a more detailed explanation, read the man pages by using the following command `man ncmpcpp` or just read the comments in the example config file.

### mpc
#### Mpc doesn't really have any configuration. The only things mpc is used for is to skip/go back a song and to do other miscelleanous multimedia and audio things. You could bind the standard mpc command (`mpc stop`, `mpc toggle`, `mpc prev`, `mpc next` etc...) to somekeybinds to have some extra functionality if you want to.

&nbsp;
&nbsp;

## Usage
#### Before launching ncmpcpp, start by launching mpd:
```
$ mpd
```
#### Once you launched mpd, launch ncmpcpp by just typing `ncmpcpp` in your terminal press `u` to update the database, which will automatically load the audio files in your music folder. To see some of the default keybinds that you can use for navigation and control visit [the project's GitHub](https://gist.github.com/ahushh/4bb5fbc38e149bfd6a08).
&nbsp;
&nbsp;
## [Go back](/posts/postsintro)
