# CV_DL

## Creazione ambiente conda

Requisito fondamentale per poter avviare il training della rete neurale è avere installato CONDA nella propria macchina locale.

## Download e setup codice librerie

I comandi che vedremo in seguito sono relativi al sistema Linux.

* Clone della repository
  * `git clone https://github.com/MalatestaDavide/CV_DL`
  
* Si estraggono i file e si entra all'interno della cartella rinominata VASTA
  * `cd VASTA`

* Creazione della cartella che conterrà i video (prima va fatto l'unzip di data.zip)
  * `mkdir data/MSRVTT/videos`

* Download dei video
  * `wget https://download2390.mediafire.com/dw26vhxfq4wg/czh8sezbo9s4692/test_videos.zip`
  * `wget https://download2280.mediafire.com/hjobfaaytmig/x3rrbe4hwp04e6w/train_val_videos.zip`
  
* Si estraggono i file e si caricano all'interno della cartella videos creata precedentemente
  * `unzip -d data/MSRVTT/videos/ test_videos.zip`
  * `unzip -d data/MSRVTT/videos/ train_val_videos.zip`

* Creazione e attivazione di un environment conda
  * `conda env update -f environment.yml -n TED`
  * `conda activate TED`
  
* Download dei pesi della rete Swin-B e creazione della cartella ceckpoint
  * `wget swin_base_patch244_window877_kinetics400_22k.pth https://github.com/SwinTransformer/storage/releases/download/v1.0.4/swin_base_patch244_window877_kinetics400_22k.pth`
   * `mkdir checkpoint checkpoint/swin`
  
* Spostamento del file all'interno della cartella creata precedentemente
  * `mv swin_base_patch244_window877_kinetics400_22k.pth checkpoint/swin/swin_base_patch244_window877_kinetics400_22k.pth` 
 
* Codici da installare per valutare la caption di un video
  * `pip install pycocoevalcap`

* Installazione della libreria apex
  * `git clone https://github.com/NVIDIA/apex`

* Si estraggono i file e si entra all'interno della cartella rinominata apex
  * `cd apex`
  
* Installazione del file setup.py
  * `python setup.py install`
  
## Train

* Torniamo all'interno della cartella VASTA ed effettuiamo il training
  * `python main.py --afs=True --dataset=msrvtt --semantics=False`
  
## Test

* Con quest'ultimo comando andiamo ad effettuare il testing
  
  * `python test.py --afs=True --dataset=msrvtt --semantics=True --bestmodel=lightning_logs/version_4/checkpoints/checkpoint-epoch=10-harmonic_mean_bleu_meteor=3.563e-01.ckpt.ckpt`
