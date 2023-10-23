# Wav2Lip

---

# Wav2Lip: Accurately Lip-syncing Videos

## Introduction
Wav2Lip is a deep learning model that takes a video with a face and an audio clip as inputs and generates a video in which the face in the video is lip-syncing to the audio. This README provides instructions on how to run the Wav2Lip model, evaluate its performance, and view sample outputs.

## Prerequisites

1. Clone the repository:
   ```bash
   git clone https://github.com/justinjohn0306/Wav2Lip
   ```
   
2. Download the pretrained models:
   ```bash
   cd Wav2Lip
   wget 'https://github.com/justinjohn0306/Wav2Lip/releases/download/models/wav2lip.pth' -O 'checkpoints/wav2lip.pth'
   wget 'https://github.com/justinjohn0306/Wav2Lip/releases/download/models/wav2lip_gan.pth' -O 'checkpoints/wav2lip_gan.pth'
   wget 'https://github.com/justinjohn0306/Wav2Lip/releases/download/models/resnet50.pth' -O 'checkpoints/resnet50.pth'
   wget 'https://github.com/justinjohn0306/Wav2Lip/releases/download/models/mobilenet.pth' -O 'checkpoints/mobilenet.pth'
   ```

3. Install necessary Python packages:
   ```bash
   pip install ffmpeg-python mediapipe==0.8.11 batch-face
   ```

## Sample Inputs and Outputs

- Sample Input Video: `input.mp4`
- Sample Input Audio: `Sync_voice_Input.wav`
- Sample Output Video: `Sample_Output.mp4`

You can view these samples to get a sense of the model's capabilities.

## Running the Model

1. Place your video (`input_vid.mp4`) in the `sample_data` directory and your audio (`input_audio.wav`) in the same directory.
  
2. Execute the inference:
   ```bash
   cd Wav2Lip
   python inference.py --checkpoint_path checkpoints/wav2lip_gan.pth --face "../sample_data/input_vid.mp4" --audio "../sample_data/input_audio.wav"
   ```

   The above command will use the HD model (`wav2lip_gan.pth`). If you prefer to use the base model, replace `wav2lip_gan.pth` with `wav2lip.pth` in the command.

3. The output video will be saved as `results/result_voice.mp4`.

## Evaluating the Model's Performance

1. Visually inspect the generated video to ensure the face is accurately lip-syncing to the audio.
2. You can use objective metrics such as L1 loss or Mean Squared Error (MSE) between the predicted lip movements and the ground truth. However, subjective evaluation (human judgment) is often more reliable for this task.
3. Compare the generated video with the original video to check for artifacts or anomalies introduced during the lip-syncing process.

## Troubleshooting

1. If you face issues with the model not detecting the face, you can adjust the padding using the `--pads` argument:
   ```bash
   --pads <top> <bottom> <left> <right>
   ```

2. If the output video's lips do not sync smoothly with the audio, you can add the `--nosmooth` flag to the inference command.

3. Ensure the audio and video are of the same duration. If not, you may need to trim or extend one of them to match the other.

---
