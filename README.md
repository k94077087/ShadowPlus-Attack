# Adversarial Attack by Shadows+

This work implements the code for "Shadow+: Edge Shadow Adversarial Attacks on Object Recognition for Autonomous Vehicles", based on modifications of the code provided in "[Shadows can be Dangerous: Stealthy and Effective Physical-world Adversarial Attack by Natural Phenomenon](https://github.com/hncszyq/ShadowAttack)". Additional references may include code from Zhong et al. 

<br>

```

## Usage of shadow_attack.py

 - **Datasets and trained models**  
   You should first download [the LISA and GTSRB datasets](https://drive.google.com/file/d/1t0czS_foldi028IV0Urf79QkdA3o3K4t/view?usp=sharing) and [our trained models](https://drive.google.com/file/d/1Rtg8HO_NA7tqCZ6HHV5PhJEzUOOv6ANA/view?usp=sharing) and place them in dataset/ and model/, respectively.  

 - **Requirements:**  
   ```text
   python = 3.11.3
   pytorch = 1.9.0
   torchvision = 0.10.0
   ```
   To run in an environment without cuda enabled, change `"device": "cuda:0"` to `"device": "cpu"` in params.json.


 - **Example 1: show help message.**
   ```shell
   $ python3 shadow_attack.py --help
   ```
   ```text
   usage: shadow_attack.py [-h] [--shadow_level SHADOW_LEVEL] [--attack_db ATTACK_DB] [--attack_type ATTACK_TYPE] [--image_path IMAGE_PATH] [--mask_path MASK_PATH] [--image_label IMAGE_LABEL] [--polygon POLYGON] [--n_try N_TRY] [--target_model TARGET_MODEL]

   optional arguments:
   -h, --help           show this help message and exit
   --shadow_level       shadow coefficient k
   --attack_db          the target dataset should be specified for a digital attack
   --attack_type        digital attack or physical attack
   --image_path         the file path to the target image should be specified for a physical attack
   --mask_path          the file path to the mask should be specified for a physical attack
   --image_label        the ground truth should be specified for a physical attack
   --polygon            The number of sides of polygon P.
   --n_try              n-random-start strategy: retry n times
   --target_model       attack normal model or robust model
   ```
   
 - **Example 2: our digital attack:**  
  The following shell will launch our digital attack on LISA while setting the shadow level $k$ as 0.43. The generated digital adversarial examples will be saved to adv_img/LISA/43/.
   ```shell
   $ python3 shadow_attack.py --shadow_level 0.43 --attack_db LISA
   ```
   ```text
   try 1: Best solution: 0.09873462468385696 succeed
   try 1: Best solution: 0.08393772691488266 succeed
   try 1: Best solution: 0.053570982068777084 succeed
   try 1: Best solution: 0.0678005963563919 succeed
   ...
   try 1: Best solution: 0.09404987096786499 succeed
   try 1: Best solution: 0.06214200705289841 succeed
   try 1: Best solution: 0.11059863865375519 succeed
   Attack finished! Success rate: 0.9822888283378747
   ```
 
 - **Example 3: Change the number of sides of polygon P, e.g., 4:**
   ```shell
   $ python3 shadow_attack.py --attack_db LISA --polygon 4
   ```
