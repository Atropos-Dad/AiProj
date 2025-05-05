# Child Face Generator
![image](https://github.com/user-attachments/assets/16310841-7167-4de9-a4ff-cddd37b91571)
![image](https://github.com/user-attachments/assets/f694c7ec-0b22-442e-9ddc-d21d8ad59bf6)

This project uses StyleGAN and encoder4editing to generate child faces from parent faces using a learned weighting model.

## Setup

1. Clone this repository:
```bash
git clone https://github.com/yourusername/child-face-generator.git
cd child-face-generator
```

2. Run the setup script to install dependencies and download required models:
```bash
python setup.py
```

This will:
- Install required Python packages
- Create necessary directories
- Clone the encoder4editing repository
- Download pretrained models
- Set up the project structure

## Project Structure

```
child-face-generator/
├── train.py              # Main training script
├── data_loader.py        # Data loading utilities
├── visualization_utils.py # Visualization functions
├── setup.py             # Setup script
├── requirements.txt     # Python dependencies
├── outputs/            # Generated outputs
├── family_models/      # Saved model checkpoints
├── embeddings/         # Face embeddings
├── latents/           # Latent codes
├── pretrained_models/  # Downloaded pretrained models
└── sample_images/     # Your input images
    ├── fathers/
    ├── mothers/
    └── children/
```

## Usage

1. Prepare your data:
   - Place father images in `sample_images/fathers/`
   - Place mother images in `sample_images/mothers/`
   - Place child images in `sample_images/children/`
   - Create a CSV file with family information (see format below)

2. Update configuration in `train.py`:
```python
config = {
    'output_dir': 'outputs',
    'model_dir': 'family_models',
    'embeddings_dir': 'embeddings',
    'base_path': 'sample_images',  # Path to your images
    'csv_path': 'path/to/your/family_data.csv',  # Your CSV file
    'latent_dir': 'latents',  # Where to save/load latent codes
    'learning_rate': 0.00001,
    'num_epochs': 80,
    'batch_size': 4,
    'use_scheduler': True
}
```

3. Run training:
```bash
python train.py
```

## CSV Format

Your family data CSV should have the following format:

```csv
family_id,father_name,mother_name,child_name,father_images,mother_images,child_images
0,John,Jane,Junior,"['father1.jpg']","['mother1.jpg']","['child1.jpg']"
1,Bob,Alice,Charlie,"['father2.jpg']","['mother2.jpg']","['child2.jpg']"
```

Where:
- `family_id`: Unique identifier for each family
- `*_name`: Names of family members
- `*_images`: Lists of image filenames (relative to base_path)

## Generated Outputs

The training process will generate:
- Training progress plots in `outputs/`
- Generated child images in `outputs/`
- Model checkpoints in `family_models/`
- Weight analysis visualizations in `outputs/`

## Requirements

- Python 3.7+
- PyTorch 1.7+
- CUDA-capable GPU (recommended)
- Other dependencies (installed by setup.py):
  - torchvision
  - numpy
  - pandas
  - Pillow
  - matplotlib
  - tqdm
  - scikit-learn
  - ninja

## Notes

- The model performs best with front-facing, well-lit facial images
- Image resolution should be consistent (recommended: 1024x1024)
- Training time depends on dataset size and GPU capabilities
- For best results, use at least 100 family sets for training

## Acknowledgments

This project uses:
- [encoder4editing](https://github.com/omertov/encoder4editing)
- StyleGAN2 architecture
- dlib face alignment 
