# YoutubeDownloader
My personal YT Downlader Notebook

## Overview

This repository contains a Jupyter Notebook designed to download YouTube videos in MP4 format using the `yt-dlp` library. The notebook provides a simple and efficient way to download videos directly to your local machine.

## Installation

To use this notebook, you need to have Python installed. Additionally, you need to install the `yt-dlp` library. You can install it using pip:

```bash
pip install yt-dlp

Usage

    Open the Notebook: Open the YoutubeDownloader.ipynb file in Jupyter Notebook.
    Run the Cells: Execute the cells in order. The first cell installs the yt-dlp library, and the second cell contains the function to download the video.
    Input the URL: Replace the youtube_url variable with the URL of the YouTube video you want to download.
    Download the Video: Run the cell containing the download_youtube_video function. The video will be downloaded in MP4 format to the specified output path.

Code Explanation

Cell 1: Install yt-dlp

!pip install yt-dlp

This cell installs the yt-dlp library, which is required to download YouTube videos.

Cell 2: Download YouTube Video

import yt_dlp

def download_youtube_video(url, output_path='.'):
    """
    Download a YouTube video given its URL in MP4 format using yt-dlp.

    Parameters:
    url (str): The URL of the YouTube video.
    output_path (str): The directory where the video will be saved. Default is the current directory.

    Returns:
    str: The path to the downloaded video file.
    """
    try:
        # Set up yt-dlp options
        ydl_opts = {
            'outtmpl': f'{output_path}/%(title)s.mp4',
            'format': 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]/best',
            'postprocessors': [{
                'key': 'FFmpegVideoConvertor',
                'preferedformat': 'mp4',  # Convert to mp4 if necessary
            }],
            'verbose': True,
        }

        # Create a yt-dlp object with the options
        with yt_dlp.YoutubeDL(ydl_opts) as ydl:
            # Download the video
            info_dict = ydl.extract_info(url, download=True)
            video_title = info_dict.get('title', 'unknown_video')
            video_path = f"{output_path}/{video_title}.mp4"

            print(f"Download completed! Saved at: {video_path}")
            return video_path

    except Exception as e:
        print(f"An error occurred: {e}")
        return None

# Example usage
youtube_url = "https://www.youtube.com/watch?v=cK0ApVxMvAM"
download_youtube_video(youtube_url)

This cell defines the download_youtube_video function, which downloads the YouTube video in MP4 format. The video URL and output path can be specified as parameters.

Example Output

When you run the notebook, you should see output similar to this:

Download completed! Saved at: ./AWS Marketplace： Private Marketplace.mp4

Notes

    Reliability: The yt-dlp library is designed to handle YouTube's dynamic content and anti-scraping measures more effectively than manual methods.
    Ethics and Legality: Ensure you have the right to download the video and use it in compliance with YouTube's policies and copyright laws.
