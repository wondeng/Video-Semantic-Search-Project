import ffmpeg
import os
import torch
from PIL import Image
from open_clip import create_model_and_transforms, tokenize


def extract_frames(video_path, output_dir, frame_rate=10):
    """
    Extract every `frame_rate`-th frame from the video.
    """
    if not os.path.exists(video_path):
        raise FileNotFoundError(f"Video file not found: {video_path}")

    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    try:
        (
            ffmpeg
            .input(video_path)
            .filter('select', f'not(mod(n\,{frame_rate}))')
            .output(f'{output_dir}/frame_%04d.png', vsync='vfr')
            .run(capture_stdout=True, capture_stderr=True)
        )
    except ffmpeg.Error as e:
        print("FFmpeg error:", e.stderr.decode())
        raise


def generate_embeddings(frame_dir):
    # Load the model and transformations
    model, _, transform = create_model_and_transforms('ViT-B-32', pretrained='openai')
    model.eval()

    embeddings = []
    for frame_file in sorted(os.listdir(frame_dir)):
        if frame_file.endswith('.png'):
            img_path = os.path.join(frame_dir, frame_file)
            image = Image.open(img_path).convert('RGB')
            image = transform(image).unsqueeze(0)  # Add batch dimension

            with torch.no_grad():
                embedding = model.encode_image(image)
                embeddings.append(embedding.cpu().numpy())
    return embeddings


if __name__ == '__main__':
    video_path = 'C:\\Users\\16467\\Videos\\Capture.mp4'  # VIDEO PATH GOES HERE
    output_dir = 'extracted_frames'

    try:
        # Extract frames
        extract_frames(video_path, output_dir)

        # Generate embeddings
        embeddings = generate_embeddings(output_dir)

        # Optionally, save embeddings to a file
        import numpy as np

        np.save('embeddings.npy', embeddings)

        print(f'Generated embeddings for {len(embeddings)} frames.')
    except FileNotFoundError as fnf_error:
        print(fnf_error)
    except Exception as e:
        print(f"An error occurred: {e}")
