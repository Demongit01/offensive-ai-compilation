# Offensive AI Compilation

A curated list of useful resources that cover Offensive AI.

- [🚫 Abuse 🚫](#-abuse-)
  - [🧠 Adversarial Machine Learning 🧠](#-adversarial-machine-learning-)
    - [⚡ Attacks ⚡](#-attacks-)
      - [🔒 Extraction 🔒](#-extraction-)
        - [⚠️ Limitations ⚠️](#️-limitations-️)
        - [🛡️ Defensive actions 🛡️](#️-defensive-actions-️)
        - [🔗 Useful links 🔗](#-useful-links-)
      - [⬅️ Inversion (or inference) ⬅️](#️-inversion-or-inference-️)
        - [🛡️ Defensive actions 🛡️](#️-defensive-actions-️-1)
        - [🔗 Useful links 🔗](#-useful-links--1)
      - [💉 Poisoning 💉](#-poisoning-)
        - [🔓 Backdoors 🔓](#-backdoors-)
        - [🛡️ Defensive actions 🛡️](#️-defensive-actions-️-2)
        - [🔗 Useful links 🔗](#-useful-links--2)
      - [🏃‍♂️ Evasion 🏃‍♂️](#️-evasion-️)
        - [🛡️ Defensive actions 🛡️](#️-defensive-actions-️-3)
        - [🔗 Useful links 🔗](#-useful-links--3)
    - [🛠️ Tools 🛠️](#️-tools-️)
        - [ART](#art)
        - [Cleverhans](#cleverhans)
- [🔧 Use 🔧](#-use-)
  - [🔊 Audio 🔊](#-audio-)
    - [🛠️ Tools 🛠️](#️-tools-️-1)
    - [💡 Applications 💡](#-applications-)
    - [🔎 Detection 🔎](#-detection-)
  - [📷 Image 📷](#-image-)
    - [🛠️ Tools 🛠️](#️-tools-️-2)
    - [💡 Applications 💡](#-applications--1)
    - [🔎 Detection 🔎](#-detection--1)
  - [🎥 Video 🎥](#-video-)
    - [🛠️ Tools 🛠️](#️-tools-️-3)
    - [💡 Applications 💡](#-applications--2)
    - [🔎 Detection 🔎](#-detection--2)
  - [📄 Text 📄](#-text-)
    - [🛠️ Tools 🛠️](#️-tools-️-4)
    - [🔎 Detection 🔎](#-detection--3)
    - [💡 Applications 💡](#-applications--3)
  - [📚 Misc 📚](#-misc-)
- [📊 Surveys 📊](#-surveys-)
- [🗣 Contributors 🗣](#-contributors-)
- [©️ License ©️](#️-license-️)

## 🚫 Abuse 🚫

Exploiting the vulnerabilities of AI models. 

### 🧠 Adversarial Machine Learning 🧠

Adversarial Machine Learning is responsible for assessing their weaknesses and providing countermeasures.

#### ⚡ Attacks ⚡

It is organized in four types of attacks: extraction, inversion, poisoning and evasion.

![Adversarial Machine Learning attacks](/assets/images/attacks.png)

##### 🔒 Extraction 🔒

It tries to steal the parameters and hyperparameters of a model by making requests that maximize the extraction of information.

![Extraction attack](/assets/images/extraction.png)

Depending on the knowledge of the adversary's model, white-box and black-box attacks can be performed.

In the simplest white-box case (when the adversary has full knowledge of the model, e.g., a sigmoid function), one can create a system of linear equations that can be easily solved.

In the generic case, where there is insufficient knowledge of the model, the substitute model is used. This model is trained with the requests made to the original model in order to imitate the same functionality as the original one.

![White-box and black-box extraction attacks](/assets/images/extraction-white-black-box.png)

###### ⚠️ Limitations ⚠️

  * Training a substitute model is equivalent (in many cases) to training a model from scratch.

  * Very computationally intensive.

  * The adversary has limitations on the number of requests before being detected.

###### 🛡️ Defensive actions 🛡️

  * Rounding of output values.

  * Use of [differential privacy](https://en.wikipedia.org/wiki/Differential_privacy).

  * Use of [ensembles](https://en.wikipedia.org/wiki/Ensemble_learning).

  * Use of specific defenses
    * [Specific architectures](https://arxiv.org/abs/1711.07221)
    * [PRADA](https://arxiv.org/abs/1805.02628)
    * [Adaptive Misinformation](https://arxiv.org/abs/1911.07100)
    * ...

###### 🔗 Useful links 🔗
  
  * [Stealing Machine Learning Models via Prediction APIs](https://arxiv.org/abs/1609.02943)
  * [Stealing Hyperparameters in Machine Learning](https://arxiv.org/abs/1802.05351)
  * [Knockoff Nets: Stealing Functionality of Black-Box Models](https://arxiv.org/abs/1812.02766)
  * [Model Extraction Warning in MLaaS Paradigm](https://arxiv.org/abs/1711.07221)
  * [Copycat CNN: Stealing Knowledge by Persuading Confession with Random Non-Labeled Data](https://arxiv.org/abs/1806.05476)
  * [Prediction Poisoning: Towards Defenses Against DNN Model Stealing Attacks](https://arxiv.org/abs/1906.10908)
  * [Stealing Neural Networks via Timing Side Channels](https://arxiv.org/abs/1812.11720)
  * [Model Stealing Attacks Against Inductive Graph Neural Networks](https://arxiv.org/abs/2112.08331)
  * [High Accuracy and High Fidelity Extraction of Neural Networks](https://arxiv.org/abs/1909.01838)
  * [Poisoning Web-Scale Training Datasets is Practical](https://arxiv.org/abs/2302.10149)

##### ⬅️ Inversion (or inference) ⬅️
  
They are intended to reverse the information flow of a machine learning model.

![Inference attack](/assets/images/inversion.png)

They enable an adversary to have knowledge of the model that was not explicitly intended to be shared.

They allow to know the training data or information as statistical properties of the model.

Three types are possible:

  * **Membership Inference Attack (MIA)**: An adversary attempts to determine whether a sample was employed as part of the training. 

  * **Property Inference Attack (PIA)**: An adversary aims to extract statistical properties that were not explicitly encoded as features during the training phase.

  * **Reconstruction**: An adversary tries to reconstruct one or more samples from the training set and/or their corresponding labels. Also called inversion.


###### 🛡️ Defensive actions 🛡️

  * Use of advanced cryptography. Countermeasures include [differential privacy](https://en.wikipedia.org/wiki/Differential_privacy), [homomorphic cryptography](https://en.wikipedia.org/wiki/Homomorphic_encryption) and [secure multiparty computation](https://en.wikipedia.org/wiki/Secure_multi-party_computation).

  * Use of regularization techniques such as [Dropout](https://en.wikipedia.org/wiki/Dilution_(neural_networks)) due to the relationship between overtraining and privacy.

  * [Model compression](https://medium.com/gsi-technology/an-overview-of-model-compression-techniques-for-deep-learning-in-space-3fd8d4ce84e5) has been proposed as a defense against reconstruction attacks.

###### 🔗 Useful links 🔗

  * [Membership Inference Attacks Against Machine Learning Models](https://arxiv.org/abs/1610.05820)
  * [Model Inversion Attacks that Exploit Confidence Information and Basic Countermeasures](https://dl.acm.org/doi/10.1145/2810103.2813677)
  * [Machine Learning Models that Remember Too Much](https://arxiv.org/abs/1709.07886)
  * [ML-Leaks: Model and Data Independent Membership Inference Attacks and Defenses on Machine Learning Models](https://arxiv.org/abs/1806.01246)
  * [Deep Models Under the GAN: Information Leakage from Collaborative Deep Learning](https://arxiv.org/abs/1702.07464)
  * [LOGAN: Membership Inference Attacks Against Generative Models](https://petsymposium.org/popets/2019/popets-2019-0008.php)
  * [Overfitting, robustness, and malicious algorithms: A study of potential causes of privacy risk in machine learning](https://content.iospress.com/articles/journal-of-computer-security/jcs191362)
  * [Comprehensive Privacy Analysis of Deep Learning: Stand-alone and Federated Learning under Passive and Active White-box Inference Attacks](https://arxiv.org/abs/1812.00910)
  * [Inference Attacks Against Collaborative Learning](https://arxiv.org/abs/1805.04049)
  * [The Secret Sharer: Evaluating and Testing Unintended Memorization in Neural Networks](https://arxiv.org/abs/1802.08232)
  * [Towards the Science of Security and Privacy in Machine Learning](https://arxiv.org/abs/1611.03814)
  * [MemGuard: Defending against Black-Box Membership Inference Attacks via Adversarial Examples](https://arxiv.org/abs/1909.10594)
  * [Property Inference Attacks on Fully Connected Neural Networks using Permutation Invariant Representations](https://dl.acm.org/doi/10.1145/3243734.3243834)
  * [Extracting Training Data from Diffusion Models](https://arxiv.org/abs/2301.13188)

##### 💉 Poisoning 💉

They aim to corrupt the training set by causing a machine learning model to reduce its accuracy.

![Poisoning attack](/assets/images/poisoning.png)

This attack is difficult to detect when performed on the training data, since the attack can propagate among different models using the same training data.

The adversary seeks to destroy the availability of the model by modifying the decision boundary and, as a result, producing incorrect predictions or, create a backdoor in a model. In the latter, the model behaves correctly (returning the desired predictions) in most cases, except for certain inputs specially created by the adversary that produce undesired results. The adversary can manipulate the results of the predictions and launch future attacks.

###### 🔓 Backdoors 🔓

[BadNets](https://arxiv.org/abs/1708.06733) are the simplest type of backdoor in a machine learning model. Moreover, BadNets are able to be preserved in a model, even if they are retrained again for a different task than the original model (transfer learning).

It is important to note that **public pre-trained models may contain backdoors**.

###### 🛡️ Defensive actions 🛡️

  * Detection of poisoned data, along with the use of data sanitization.

  * Robust training methods.

  * Specific defenses.
    * [Neural Cleanse: Identifying and Mitigating Backdoor Attacks in Neural Networks](https://ieeexplore.ieee.org/document/8835365) 
    * [STRIP: A Defence Against Trojan Attacks on Deep Neural Networks](https://arxiv.org/abs/1902.06531)
    * [Detecting Backdoor Attacks on Deep Neural Networks by Activation Clustering](https://arxiv.org/abs/1811.03728)
    * [ABS: Scanning Neural Networks for Back-doors by Artificial Brain Stimulation](https://dl.acm.org/doi/10.1145/3319535.3363216)
    * [DeepInspect: A Black-box Trojan Detection and Mitigation Framework for Deep Neural Networks](https://www.ijcai.org/proceedings/2019/647)
    * [Defending Neural Backdoors via Generative Distribution Modeling](https://arxiv.org/abs/1910.04749)

###### 🔗 Useful links 🔗

  * [Poisoning Attacks against Support Vector Machines](https://arxiv.org/abs/1206.6389)
  * [Targeted Backdoor Attacks on Deep Learning Systems Using Data Poisoning](https://arxiv.org/abs/1712.05526)
  * [Trojaning Attack on Neural Networks](https://www.semanticscholar.org/paper/Trojaning-Attack-on-Neural-Networks-Liu-Ma/08f7ac64b420210aa46fcbbdb0f206215f2e0644)
  * [Fine-Pruning: Defending Against Backdooring Attacks on Deep Neural Networks](https://arxiv.org/abs/1805.12185)
  * [Poison Frogs! Targeted Clean-Label Poisoning Attacks on Neural Networks](https://arxiv.org/abs/1804.00792)
  * [Spectral Signatures in Backdoor Attacks](https://arxiv.org/abs/1811.00636)
  * [Latent Backdoor Attacks on Deep Neural Networks](https://dl.acm.org/doi/10.1145/3319535.3354209)
  * [Regula Sub-rosa: Latent Backdoor Attacks on Deep Neural Networks](https://arxiv.org/abs/1905.10447)
  * [Hidden Trigger Backdoor Attacks](https://arxiv.org/abs/1910.00033)
  * [Transferable Clean-Label Poisoning Attacks on Deep Neural Nets](https://arxiv.org/abs/1905.05897)
  * [TABOR: A Highly Accurate Approach to Inspecting and Restoring Trojan Backdoors in AI Systems](https://arxiv.org/abs/1908.01763)
  * [Towards Poisoning of Deep Learning Algorithms with Back-gradient Optimization](https://arxiv.org/abs/1708.08689)
  * [When Does Machine Learning FAIL? Generalized Transferability for Evasion and Poisoning Attacks](https://arxiv.org/abs/1803.06975)
  * [Certified Defenses for Data Poisoning Attacks](https://arxiv.org/abs/1706.03691)
  * [Input-Aware Dynamic Backdoor Attack](https://arxiv.org/abs/2010.08138)
  * [How To Backdoor Federated Learning](https://arxiv.org/abs/1807.00459)
  * [Planting Undetectable Backdoors in Machine Learning Models](https://arxiv.org/abs/2204.06974)
  * [Fool the AI!](https://fooltheai.mybluemix.net/): Hackers can use backdoors to poison training data and cause an AI model to misclassify images. Learn how IBM researchers can tell when data has been poisoned, then guess what backdoors have been hidden in these datasets. Can you guess the backdoor?

##### 🏃‍♂️ Evasion 🏃‍♂️

An adversary adds a small perturbation (in the form of noise) to the input of a machine learning model to make it classify incorrectly (example adversary).

![Evasion attack](/assets/images/evasion.png)

They are similar to poisoning attacks, but their main difference is that evasion attacks try to exploit weaknesses of the model in the inference phase. 

The goal of the adversary is for adversarial examples to be imperceptible to a human.

Two types of attack can be performed depending on the output desired by the opponent:

  * **Targeted**: the adversary aims to obtain a prediction of his choice.

    ![Targeted attack](/assets/images/targeted.png)

  * **Untargeted**: the adversary intends to achieve a misclassification.

    ![Untargeted attack](/assets/images/untargeted.png)

The most common attacks are **white-box attacks**:

  * [L-BFGS](https://arxiv.org/abs/1312.6199)
  * [FGSM](https://arxiv.org/abs/1412.6572)
  * [BIM](https://arxiv.org/abs/1607.02533)
  * [JSMA](https://arxiv.org/abs/1511.07528)
  * [Carlini & Wagner (C&W)](https://arxiv.org/abs/1608.04644)
  * [NewtonFool](https://andrewxiwu.github.io/public/papers/2017/JWJ17-objective-metrics-and-gradient-descent-based-algorithms-for-adversarial-examples-in-machine-learning.pdf)
  * [EAD](https://arxiv.org/abs/1709.04114)
  * [UAP](https://arxiv.org/abs/1610.08401)

###### 🛡️ Defensive actions 🛡️

  * Adversarial training, which consists of crafting adversarial examples during training so as to allow the model to learn features of the adversarial examples, making the model more robust to this type of attack.

  * Transformations on inputs.

  * Gradient masking/regularization. [Not very effective](https://arxiv.org/abs/1802.00420).

  * Weak defenses.

###### 🔗 Useful links 🔗

  * [Practical Black-Box Attacks against Machine Learning](https://arxiv.org/abs/1602.02697)
  * [The Limitations of Deep Learning in Adversarial Settings](https://arxiv.org/abs/1511.07528)
  * [Towards Evaluating the Robustness of Neural Networks](https://arxiv.org/abs/1608.04644)
  * [Distillation as a Defense to Adversarial Perturbations Against Deep Neural Networks](https://arxiv.org/abs/1511.04508)
  * [Adversarial examples in the physical world](https://arxiv.org/abs/1607.02533)
  * [Ensemble Adversarial Training: Attacks and Defenses](https://arxiv.org/abs/1705.07204)
  * [Towards Deep Learning Models Resistant to Adversarial Attacks](https://arxiv.org/abs/1706.06083)
  * [Intriguing properties of neural networks](https://arxiv.org/abs/1312.6199)
  * [Explaining and Harnessing Adversarial Examples](https://arxiv.org/abs/1412.6572)
  * [Delving into Transferable Adversarial Examples and Black-box Attacks](https://arxiv.org/abs/1611.02770)
  * [Black-box Adversarial Attacks with Limited Queries and Information](https://arxiv.org/abs/1804.08598)
  * [Feature Squeezing: Detecting Adversarial Examples in Deep Neural Networks](https://arxiv.org/abs/1704.01155)
  * [Decision-Based Adversarial Attacks: Reliable Attacks Against Black-Box Machine Learning Models](https://arxiv.org/abs/1712.04248)
  * [Boosting Adversarial Attacks with Momentum](https://openaccess.thecvf.com/content_cvpr_2018/papers/Dong_Boosting_Adversarial_Attacks_CVPR_2018_paper.pdf)
  * [The Space of Transferable Adversarial Examples](https://arxiv.org/abs/1704.03453)
  * [Countering Adversarial Images using Input Transformations](https://arxiv.org/abs/1711.00117)
  * [Defense-GAN: Protecting Classifiers Against Adversarial Attacks Using Generative Models](https://arxiv.org/abs/1805.06605)
  * [Synthesizing Robust Adversarial Examples](https://arxiv.org/abs/1707.07397)
  * [Mitigating adversarial effects through randomization](https://arxiv.org/abs/1711.01991)
  * [On Detecting Adversarial Perturbations](https://arxiv.org/abs/1702.04267)
  * [PixelDefend: Leveraging Generative Models to Understand and Defend against Adversarial Examples](https://arxiv.org/abs/1710.10766)
  * [One Pixel Attack for Fooling Deep Neural Networks](https://arxiv.org/abs/1710.08864)
  * [Efficient Defenses Against Adversarial Attacks](https://arxiv.org/abs/1707.06728)
  * [Robust Physical-World Attacks on Deep Learning Visual Classification](https://ieeexplore.ieee.org/document/8578273)
  * [Adversarial Perturbations Against Deep Neural Networks for Malware Classification](https://arxiv.org/abs/1606.04435)
  * [3D Adversarial Attacks Beyond Point Cloud](https://arxiv.org/abs/2104.12146)
  * [Adversarial Perturbations Fool Deepfake Detectors](https://arxiv.org/abs/2003.10596)
  * [Adversarial Deepfakes: Evaluating Vulnerability of Deepfake Detectors to Adversarial Examples](https://arxiv.org/abs/2002.12749)
  * [An Overview of Vulnerabilities of Voice Controlled Systems](https://arxiv.org/abs/1803.09156)
  * [FastWordBug: A Fast Method To Generate Adversarial Text Against NLP Applications](https://arxiv.org/abs/2002.00760)
  * [Phantom of the ADAS: Securing Advanced Driver Assistance Systems from Split-Second Phantom Attacks](https://www.nassiben.com/phantoms)

#### 🛠️ Tools 🛠️

| Name | Type | Supported algorithms | Supported attack types | Attack/Defence | Supported frameworks | Popularity |
| ---------- | :----------: | :----------: | :----------: | :----------: | :----------: | :----------: |
| [Cleverhans](https://github.com/cleverhans-lab/cleverhans) | Image | Deep Learning | Evasion | Attack | Tensorflow, Keras, JAX | [![stars](https://badgen.net/github/stars/cleverhans-lab/cleverhans)](https://github.com/cleverhans-lab/cleverhans)|
| [Foolbox](https://github.com/bethgelab/foolbox) | Image | Deep Learning | Evasion | Attack | Tensorflow, PyTorch, JAX | [![stars](https://badgen.net/github/stars/bethgelab/foolbox)](https://github.com/bethgelab/foolbox)|
| [ART](https://github.com/Trusted-AI/adversarial-robustness-toolbox) | Any type (image, tabular data, audio,...) | Deep Learning, SVM, LR, etc. | Any (extraction, inference, poisoning, evasion) | Both | Tensorflow, Keras, Pytorch, Scikit Learn | [![stars](https://badgen.net/github/stars/Trusted-AI/adversarial-robustness-toolbox)](https://github.com/Trusted-AI/adversarial-robustness-toolbox)|
| [TextAttack](https://github.com/QData/TextAttack) | Text | Deep Learning | Evasion | Attack | Keras, HuggingFace | [![stars](https://badgen.net/github/stars/QData/TextAttack)](https://github.com/QData/TextAttack)|
| [Advertorch](https://github.com/BorealisAI/advertorch) | Image | Deep Learning | Evasion | Both | --- | [![stars](https://badgen.net/github/stars/BorealisAI/advertorch)](https://github.com/BorealisAI/advertorch)|
| [AdvBox](https://github.com/advboxes/AdvBox) | Image | Deep Learning | Evasion | Both | PyTorch, Tensorflow, MxNet | [![stars](https://badgen.net/github/stars/advboxes/AdvBox)](https://github.com/advboxes/AdvBox)|
| [DeepRobust](https://github.com/DSE-MSU/DeepRobust) | Image, graph | Deep Learning | Evasion | Both | PyTorch | [![stars](https://badgen.net/github/stars/DSE-MSU/DeepRobust)](https://github.com/DSE-MSU/DeepRobust)|
| [Counterfit](https://github.com/Azure/counterfit) | Any | Any | Evasion | Attack | --- | [![stars](https://badgen.net/github/stars/Azure/counterfit)](https://github.com/Azure/counterfit)|
| [Adversarial Audio Examples](https://github.com/carlini/audio_adversarial_examples) | Audio | DeepSpeech | Evasion | Attack | --- | [![stars](https://badgen.net/github/stars/carlini/audio_adversarial_examples)](https://github.com/carlini/audio_adversarial_examples)|

###### ART

[Adversarial Robustness Toolbox](https://github.com/Trusted-AI/adversarial-robustness-toolbox), abbreviated as ART, is an open-source Adversarial Machine Learning library for testing the robustness of machine learning models.

![ART logo](/assets/images/art.png)

It is developed in Python and implements extraction, inversion, poisoning and evasion attacks and defenses.

ART supports the most popular frameworks: Tensorflow, Keras, PyTorch, MxNet, ScikitLearn, among many others.

It is not limited to the use of models that use images as input, but also supports other types of data, such as audio, video, tabular data, etc.

> [Workshop to learn Adversarial Machine Learning with ART 🇪🇸](https://github.com/jiep/adversarial-machine-learning)

###### Cleverhans

[Cleverhans](https://github.com/cleverhans-lab/cleverhans) is a library for performing evasion attacks and testing the robustness of a deep learning model on image models.

![Cleverhans logo](/assets/images/cleverhans.png)

It is developed in Python and integrates with the Tensorflow, Torch and JAX frameworks.

It implements numerous attacks such as L-BFGS, FGSM, JSMA, C&W, among others.

## 🔧 Use 🔧

Improving classic techniques with AI

### 🔊 Audio 🔊

#### 🛠️ Tools 🛠️
  * [deep-voice-conversion](https://github.com/andabi/deep-voice-conversion): Deep neural networks for voice conversion (voice style transfer) in Tensorflow. [![stars](https://badgen.net/github/stars/andabi/deep-voice-conversion)](https://github.com/andabi/deep-voice-conversion)
  * [tacotron](https://github.com/keithito/tacotron): A TensorFlow implementation of Google's Tacotron speech synthesis with pre-trained model (unofficial). [![stars](https://badgen.net/github/stars/keithito/tacotron)](https://github.com/keithito/tacotron)
  * [Real-Time-Voice-Cloning](https://github.com/CorentinJ/Real-Time-Voice-Cloning): Clone a voice in 5 seconds to generate arbitrary speech in real-time. [![stars](https://badgen.net/github/stars/CorentinJ/Real-Time-Voice-Cloning)](https://github.com/CorentinJ/Real-Time-Voice-Cloning)
  * [mimic2](https://github.com/MycroftAI/mimic2): Text to Speech engine based on the Tacotron architecture, initially implemented by Keith Ito. [![stars](https://badgen.net/github/stars/MycroftAI/mimic2)](https://github.com/MycroftAI/mimic2)
  * [Neural-Voice-Cloning-with-Few-Samples](https://github.com/Sharad24/Neural-Voice-Cloning-with-Few-Samples): Implementation of Neural Voice Cloning with Few Samples Research Paper by Baidu. [![stars](https://badgen.net/github/stars/Sharad24/Neural-Voice-Cloning-with-Few-Samples)](https://github.com/Sharad24/Neural-Voice-Cloning-with-Few-Samples)
  * [Vall-E](https://github.com/enhuiz/vall-e): An unofficial PyTorch implementation of the audio LM VALL-E. [![stars](https://badgen.net/github/stars/enhuiz/vall-e)](https://github.com/enhuiz/vall-e)

#### 💡 Applications 💡

  * [Lip2Wav](https://github.com/Rudrabha/Lip2Wav): Generate high quality speech from only lip movements. [![stars](https://badgen.net/github/stars/Rudrabha/Lip2Wav)](https://github.com/Rudrabha/Lip2Wav)
  * [AudioLDM: Text-to-Audio Generation with Latent Diffusion Models](https://huggingface.co/spaces/haoheliu/audioldm-text-to-audio-generation)
  * [deepvoice3_pytorch](https://github.com/r9y9/deepvoice3_pytorch): PyTorch implementation of convolutional neural networks-based text-to-speech synthesis models. [![stars](https://badgen.net/github/stars/r9y9/deepvoice3_pytorch)](https://github.com/r9y9/deepvoice3_pytorch)
  * [🎸 Riffusion](https://github.com/riffusion/riffusion): Stable diffusion for real-time music generation. [![stars](https://badgen.net/github/stars/riffusion/riffusion)](https://github.com/riffusion/riffusion)
  * [whisper.cpp](https://github.com/ggerganov/whisper.cpp): Port of OpenAI's Whisper model in C/C++. [![stars](https://badgen.net/github/stars/ggerganov/whisper.cpp)](https://github.com/ggerganov/whisper.cpp)
  * [TTS](https://github.com/coqui-ai/TTS): 🐸💬 - a deep learning toolkit for Text-to-Speech, battle-tested in research and production. [![stars](https://badgen.net/github/stars/coqui-ai/TTS)](https://github.com/coqui-ai/TTS)
  * [YourTTS](https://github.com/Edresson/YourTTS): Towards Zero-Shot Multi-Speaker TTS and Zero-Shot Voice Conversion for everyone. [![stars](https://badgen.net/github/stars/Edresson/YourTTS)](https://github.com/Edresson/YourTTS)
  * [TorToiSe](https://github.com/neonbjb/tortoise-tts): A multi-voice TTS system trained with an emphasis on quality. [![stars](https://badgen.net/github/stars/neonbjb/tortoise-tts)](https://github.com/neonbjb/tortoise-tts)
  * [DiffSinger](https://github.com/MoonInTheRiver/DiffSinger): Singing Voice Synthesis via Shallow Diffusion Mechanism (SVS & TTS). [![stars](https://badgen.net/github/stars/MoonInTheRiver/DiffSinger)](https://github.com/MoonInTheRiver/DiffSinger)
  * [WaveNet vocoder](https://github.com/r9y9/wavenet_vocoder): Implementation of the WaveNet vocoder, which can generate high quality raw speech samples conditioned on linguistic or acoustic features. [![stars](https://badgen.net/github/stars/r9y9/wavenet_vocoder)](https://github.com/r9y9/wavenet_vocoder)
  * [Deepvoice3_pytorch](https://github.com/r9y9/deepvoice3_pytorch): PyTorch implementation of convolutional neural networks-based text-to-speech synthesis models. [![stars](https://badgen.net/github/stars/r9y9/deepvoice3_pytorch)](https://github.com/r9y9/deepvoice3_pytorch)
  * [eSpeak NG Text-to-Speech](https://github.com/espeak-ng/espeak-ng): eSpeak NG is an open source speech synthesizer that supports more than hundred languages and accents. [![stars](https://badgen.net/github/stars/espeak-ng/espeak-ng)](https://github.com/espeak-ng/espeak-ng)
  * [Neural Voice Cloning with a Few Samples](https://proceedings.neurips.cc/paper/2018/hash/4559912e7a94a9c32b09d894f2bc3c82-Abstract.html)
  * [NAUTILUS: A Versatile Voice Cloning System](https://ieeexplore.ieee.org/abstract/document/9246264)
  * [Learning to Speak Fluently in a Foreign Language: Multilingual Speech Synthesis and Cross-Language Voice Cloning](https://arxiv.org/abs/1907.04448)
  * [When Good Becomes Evil: Keystroke Inference with Smartwatch](https://dl.acm.org/doi/10.1145/2810103.2813668)
  * [KeyListener: Inferring Keystrokes on QWERTY Keyboard of Touch Screen through Acoustic Signals](https://ieeexplore.ieee.org/document/8737591)
  * [This Voice Does Not Exist: On Voice Synthesis, Audio Deepfakes and Their Detection](https://this-voice-does-not-exist.com)


#### 🔎 Detection 🔎
  * [fake-voice-detection](https://github.com/dessa-oss/fake-voice-detection): Using temporal convolution to detect Audio Deepfakes. [![stars](https://badgen.net/github/stars/dessa-oss/fake-voice-detection)](https://github.com/dessa-oss/fake-voice-detection)
  * [A robust voice spoofing detection system using novel CLS-LBP features and LSTM](https://www.sciencedirect.com/science/article/pii/S1319157822000684)
  * [Voice spoofing detector: A unified anti-spoofing framework](https://www.sciencedirect.com/science/article/abs/pii/S0957417422002330)
  * [Securing Voice-Driven Interfaces Against Fake (Cloned) Audio Attacks](https://ieeexplore.ieee.org/abstract/document/8695320)
  * [DeepSonar: Towards Effective and Robust Detection of AI-Synthesized Fake Voices](https://dl.acm.org/doi/abs/10.1145/3394171.3413716)
  * [Fighting AI with AI: Fake Speech Detection Using Deep Learning](https://www.aes.org/e-lib/online/browse.cfm?elib=20479)
  * [A Review of Modern Audio Deepfake Detection Methods: Challenges and Future Directions](https://www.mdpi.com/1999-4893/15/5/155)

### 📷 Image 📷

#### 🛠️ Tools 🛠️

  * [StyleGAN](https://github.com/NVlabs/stylegan): StyleGAN - Official TensorFlow Implementation. [![stars](https://badgen.net/github/stars/NVlabs/stylegan)](https://github.com/NVlabs/stylegan)
  * [StyleGAN2](https://github.com/NVlabs/stylegan2): StyleGAN2 - Official TensorFlow Implementation. [![stars](https://badgen.net/github/stars/NVlabs/stylegan2)](https://github.com/NVlabs/stylegan2)
  * [stylegan2-ada-pytorch](https://github.com/NVlabs/stylegan2-ada-pytorch): StyleGAN2-ADA - Official PyTorch implementation. [![stars](https://badgen.net/github/stars/NVlabs/stylegan2-ada-pytorch)](https://github.com/NVlabs/stylegan2-ada-pytorch) 
  * [StyleGAN-nada](https://github.com/rinongal/StyleGAN-nada): CLIP-Guided Domain Adaptation of Image Generators. [![stars](https://badgen.net/github/stars/rinongal/StyleGAN-nada)](https://github.com/rinongal/StyleGAN-nada)
  * [StyleGAN3](https://github.com/NVlabs/stylegan3): Official PyTorch implementation of StyleGAN3. [![stars](https://badgen.net/github/stars/NVlabs/stylegan3)](https://github.com/NVlabs/stylegan3)
  * [Imaginaire](https://github.com/NVlabs/imaginaire): Imaginaire is a pytorch library that contains optimized implementation of several image and video synthesis methods developed at NVIDIA. [![stars](https://badgen.net/github/stars/NVlabs/imaginaire)](https://github.com/NVlabs/imaginaire)
  * [ffhq-dataset](https://github.com/NVlabs/ffhq-dataset): Flickr-Faces-HQ Dataset (FFHQ). [![stars](https://badgen.net/github/stars/NVlabs/ffhq-dataset)](https://github.com/NVlabs/ffhq-dataset)
  * [DALLE2-pytorch](https://github.com/lucidrains/DALLE2-pytorch): Implementation of DALL-E 2, OpenAI's updated text-to-image synthesis neural network, in Pytorch. [![stars](https://badgen.net/github/stars/lucidrains/DALLE2-pytorch)](https://github.com/lucidrains/DALLE2-pytorch)
  * [ImaginAIry](https://github.com/brycedrennan/imaginAIry): AI imagined images. Pythonic generation of stable diffusion images. [![stars](https://badgen.net/github/stars/brycedrennan/imaginAIry)](https://github.com/brycedrennan/imaginAIry)
  * [Lama Cleaner](https://github.com/Sanster/lama-cleaner): Image inpainting tool powered by SOTA AI Model. Remove any unwanted object, defect, people from your pictures or erase and replace(powered by stable diffusion) any thing on your pictures. [![stars](https://badgen.net/github/stars/Sanster/lama-cleaner)](https://github.com/Sanster/lama-cleaner)
  * [Invertible-Image-Rescaling](https://github.com/pkuxmq/Invertible-Image-Rescaling): This is the PyTorch implementation of paper: Invertible Image Rescaling. [![stars](https://badgen.net/github/stars/pkuxmq/Invertible-Image-Rescaling)](https://github.com/pkuxmq/Invertible-Image-Rescaling)
  * [DifFace](https://github.com/zsyOAOA/DifFace): Blind Face Restoration with Diffused Error Contraction (PyTorch). [![stars](https://badgen.net/github/stars/zsyOAOA/DifFace)](https://github.com/zsyOAOA/DifFace)
  * [CodeFormer](https://github.com/sczhou/CodeFormer): Towards Robust Blind Face Restoration with Codebook Lookup Transformer. [![stars](https://badgen.net/github/stars/sczhou/CodeFormer)](https://github.com/sczhou/CodeFormer)
  * [Custom Diffusion](https://github.com/adobe-research/custom-diffusion): Multi-Concept Customization of Text-to-Image Diffusion. [![stars](https://badgen.net/github/stars/adobe-research/custom-diffusion)](https://github.com/adobe-research/custom-diffusion)
  * [Diffusers](https://github.com/huggingface/diffusers): 🤗 Diffusers: State-of-the-art diffusion models for image and audio generation in PyTorch. [![stars](https://badgen.net/github/stars/huggingface/diffusers)](https://github.com/huggingface/diffusers)
  * [Stable Diffusion](https://github.com/Stability-AI/stablediffusion): High-Resolution Image Synthesis with Latent Diffusion Models. [![stars](https://badgen.net/github/stars/Stability-AI/stablediffusion)](https://github.com/Stability-AI/stablediffusion)
  * [InvokeAI](https://github.com/invoke-ai/InvokeAI): InvokeAI is a leading creative engine for Stable Diffusion models, empowering professionals, artists, and enthusiasts to generate and create visual media using the latest AI-driven technologies. The solution offers an industry leading WebUI, supports terminal use through a CLI, and serves as the foundation for multiple commercial products. [![stars](https://badgen.net/github/stars/invoke-ai/InvokeAI)](https://github.com/invoke-ai/InvokeAI)
  * [Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui): Stable Diffusion web UI. [![stars](https://badgen.net/github/stars/AUTOMATIC1111/stable-diffusion-webui)](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
  * [Stable Diffusion Infinity](https://github.com/lkwq007/stablediffusion-infinity): Outpainting with Stable Diffusion on an infinite canvas. [![stars](https://badgen.net/github/stars/lkwq007/stablediffusion-infinity)](https://github.com/lkwq007/stablediffusion-infinity)
  * [Fast Stable Diffusion](https://github.com/TheLastBen/fast-stable-diffusion): fast-stable-diffusion + DreamBooth. [![stars](https://badgen.net/github/stars/TheLastBen/fast-stable-diffusion)](https://github.com/TheLastBen/fast-stable-diffusion)
  * [GET3D](https://github.com/nv-tlabs/GET3D): A Generative Model of High Quality 3D Textured Shapes Learned from Images. [![stars](https://badgen.net/github/stars/nv-tlabs/GET3D)](https://github.com/nv-tlabs/GET3D)
  * [Awesome AI Art Image Synthesis](https://github.com/altryne/awesome-ai-art-image-synthesis): A list of awesome tools, ideas, prompt engineering tools, colabs, models, and helpers for the prompt designer playing with aiArt and image synthesis. Covers Dalle2, MidJourney, StableDiffusion, and open source tools. [![stars](https://badgen.net/github/stars/altryne/awesome-ai-art-image-synthesis)](https://github.com/altryne/awesome-ai-art-image-synthesis)
  * [Stable Diffusion](https://github.com/CompVis/stable-diffusion): A latent text-to-image diffusion model. [![stars](https://badgen.net/github/stars/CompVis/stable-diffusion)](https://github.com/CompVis/stable-diffusion)
  * [Weather Diffusion](https://github.com/IGITUGraz/WeatherDiffusion): Code for "Restoring Vision in Adverse Weather Conditions with Patch-Based Denoising Diffusion Models". [![stars](https://badgen.net/github/stars/IGITUGraz/WeatherDiffusion)](https://github.com/IGITUGraz/WeatherDiffusion)
  * [DF-GAN](https://github.com/tobran/DF-GAN): A Simple and Effective Baseline for Text-to-Image Synthesis. [![stars](https://badgen.net/github/stars/tobran/DF-GAN)](https://github.com/tobran/DF-GAN)
  * [Dall-E Playground](https://github.com/saharmor/dalle-playground): A playground to generate images from any text prompt using Stable Diffusion (past: using DALL-E Mini). [![stars](https://badgen.net/github/stars/saharmor/dalle-playground)](https://github.com/saharmor/dalle-playground)
  * [MM-CelebA-HQ-Dataset](https://github.com/IIGROUP/MM-CelebA-HQ-Dataset): A large-scale face image dataset that allows text-to-image generation, text-guided image manipulation, sketch-to-image generation, GANs for face generation and editing, image caption, and VQA. [![stars](https://badgen.net/github/stars/IIGROUP/MM-CelebA-HQ-Dataset)](https://github.com/IIGROUP/MM-CelebA-HQ-Dataset)
  * [Deep Daze](https://github.com/lucidrains/deep-daze): Simple command line tool for text to image generation using OpenAI's CLIP and Siren (Implicit neural representation network). [![stars](https://badgen.net/github/stars/lucidrains/deep-daze)](https://github.com/lucidrains/deep-daze)
  * [StyleMapGAN](https://github.com/naver-ai/StyleMapGAN): Exploiting Spatial Dimensions of Latent in GAN for Real-time Image Editing. [![stars](https://badgen.net/github/stars/naver-ai/StyleMapGAN)](https://github.com/naver-ai/StyleMapGAN)

#### 💡 Applications 💡

  * [ArtLine](https://github.com/vijishmadhavan/ArtLine): A Deep Learning based project for creating line art portraits. [![stars](https://badgen.net/github/stars/vijishmadhavan/ArtLine)](https://github.com/vijishmadhavan/ArtLine)
  * [Depix](https://github.com/beurtschipper/Depix): Recovers passwords from pixelized screenshots. [![stars](https://badgen.net/github/stars/beurtschipper/Depix)](https://github.com/beurtschipper/Depix)
  * [Bringing Old Photos Back to Life](https://github.com/microsoft/Bringing-Old-Photos-Back-to-Life): Old Photo Restoration (Official PyTorch Implementation). [![stars](https://badgen.net/github/stars/microsoft/Bringing-Old-Photos-Back-to-Life)](https://github.com/microsoft/Bringing-Old-Photos-Back-to-Life)
  * [Rewriting](https://github.com/davidbau/rewriting): Interactive tool to directly edit the rules of a GAN to synthesize scenes with objects added, removed, or altered. Change StyleGANv2 to make extravagant eyebrows, or horses wearing hats. [![stars](https://badgen.net/github/stars/davidbau/rewriting)](https://github.com/davidbau/rewriting)
  * [Fawkes](https://github.com/Shawn-Shan/fawkes): Privacy preserving tool against facial recognition systems. [![stars](https://badgen.net/github/stars/Shawn-Shan/fawkes)](https://github.com/Shawn-Shan/fawkes)
  * [Pulse](https://github.com/adamian98/pulse): Self-Supervised Photo Upsampling via Latent Space Exploration of Generative Models. [![stars](https://badgen.net/github/stars/adamian98/pulse)](https://github.com/adamian98/pulse)
  * [HiDT](https://github.com/saic-mdal/HiDT): Official repository for the paper "High-Resolution Daytime Translation Without Domain Labels". [![stars](https://badgen.net/github/stars/saic-mdal/HiDT)](https://github.com/saic-mdal/HiDT)
  * [3D Photo Inpainting](https://github.com/vt-vl-lab/3d-photo-inpainting): 3D Photography using Context-aware Layered Depth Inpainting. [![stars](https://badgen.net/github/stars/vt-vl-lab/3d-photo-inpainting)](https://github.com/vt-vl-lab/3d-photo-inpainting)
  * [SteganoGAN](https://github.com/DAI-Lab/SteganoGAN): SteganoGAN is a tool for creating steganographic images using adversarial training. [![stars](https://badgen.net/github/stars/DAI-Lab/SteganoGAN)](https://github.com/DAI-Lab/SteganoGAN)
  * [Stylegan-T](https://github.com/autonomousvision/stylegan-t): Unlocking the Power of GANs for Fast Large-Scale Text-to-Image Synthesis. [![stars](https://badgen.net/github/stars/autonomousvision/stylegan-t)](https://github.com/autonomousvision/stylegan-t)
  * [MegaPortraits](https://github.com/SamsungLabs/MegaPortraits): One-shot Megapixel Neural Head Avatars. [![stars](https://badgen.net/github/stars/SamsungLabs/MegaPortraits)](https://github.com/SamsungLabs/MegaPortraits)
  * [eg3d](https://github.com/NVlabs/eg3d): Efficient Geometry-aware 3D Generative Adversarial Networks. [![stars](https://badgen.net/github/stars/NVlabs/eg3d)](https://github.com/NVlabs/eg3d)
  * [TediGAN](https://github.com/IIGROUP/TediGAN): Pytorch implementation for TediGAN: Text-Guided Diverse Face Image Generation and Manipulation. [![stars](https://badgen.net/github/stars/IIGROUP/TediGAN)](https://github.com/IIGROUP/TediGAN)
  * [DALLE-pytorch](https://github.com/lucidrains/DALLE-pytorch): Implementation / replication of DALL-E, OpenAI's Text to Image Transformer, in Pytorch. [![stars](https://badgen.net/github/stars/lucidrains/DALLE-pytorch)](https://github.com/lucidrains/DALLE-pytorch)
  * [StyleNeRF](https://github.com/facebookresearch/StyleNeRF): This is the open source implementation of the ICLR2022 paper "StyleNeRF: A Style-based 3D-Aware Generator for High-resolution Image Synthesis". [![stars](https://badgen.net/github/stars/facebookresearch/StyleNeRF)](https://github.com/facebookresearch/StyleNeRF)
  * [DeepSVG](https://github.com/alexandre01/deepsvg): Official code for the paper "DeepSVG: A Hierarchical Generative Network for Vector Graphics Animation". Includes a PyTorch library for deep learning with SVG data. [![stars](https://badgen.net/github/stars/alexandre01/deepsvg)](https://github.com/alexandre01/deepsvg)
  * [NUWA](https://github.com/microsoft/NUWA): A unified 3D Transformer Pipeline for visual synthesis. [![stars](https://badgen.net/github/stars/microsoft/NUWA)](https://github.com/microsoft/NUWA)
  * [Image-Super-Resolution-via-Iterative-Refinement](https://github.com/Janspiry/Image-Super-Resolution-via-Iterative-Refinement): Unofficial implementation of Image Super-Resolution via Iterative Refinement by Pytorch. [![stars](https://badgen.net/github/stars/Janspiry/Image-Super-Resolution-via-Iterative-Refinement)](https://github.com/Janspiry/Image-Super-Resolution-via-Iterative-Refinement)
  * [Lama](https://github.com/saic-mdal/lama): 🦙 LaMa Image Inpainting, Resolution-robust Large Mask Inpainting with Fourier Convolutions. [![stars](https://badgen.net/github/stars/saic-mdal/lama)](https://github.com/saic-mdal/lama)
  * [Person_reID_baseline_pytorch](https://github.com/layumi/Person_reID_baseline_pytorch): Pytorch ReID: A tiny, friendly, strong pytorch implement of object re-identification baseline. [![stars](https://badgen.net/github/stars/layumi/Person_reID_baseline_pytorch)](https://github.com/layumi/Person_reID_baseline_pytorch)
  * [instruct-pix2pix](https://github.com/timothybrooks/instruct-pix2pix): PyTorch implementation of InstructPix2Pix, an instruction-based image editing model. [![stars](https://badgen.net/github/stars/timothybrooks/instruct-pix2pix)](https://github.com/timothybrooks/instruct-pix2pix)
  * [GFPGAN](https://github.com/TencentARC/GFPGAN): GFPGAN aims at developing Practical Algorithms for Real-world Face Restoration. [![stars](https://badgen.net/github/stars/TencentARC/GFPGAN)](https://github.com/TencentARC/GFPGAN)
  * [DeepVecFont](https://github.com/yizhiwang96/deepvecfont): Synthesizing High-quality Vector Fonts via Dual-modality Learning. [![stars](https://badgen.net/github/stars/yizhiwang96/deepvecfont)](https://github.com/yizhiwang96/deepvecfont)
  * [Stargan v2 Tensorflow](https://github.com/clovaai/stargan-v2-tensorflow): Official Tensorflow Implementation. [![stars](https://badgen.net/github/stars/clovaai/stargan-v2-tensorflow)](https://github.com/clovaai/stargan-v2-tensorflow)
  * [StyleGAN2 Distillation](https://github.com/EvgenyKashin/stylegan2-distillation): Paired image-to-image translation, trained on synthetic data generated by StyleGAN2 outperforms existing approaches in image manipulation. [![stars](https://badgen.net/github/stars/EvgenyKashin/stylegan2-distillation)](https://github.com/EvgenyKashin/stylegan2-distillation)
  * [Extracting Training Data from Diffusion Models](https://arxiv.org/abs/2301.13188)
  * [Mann-E - Mann-E (Persian: مانی) is an art generator model based on the weights of Stable Diffusion 1.5 and data gathered from artistic material available on Pinterest](https://opencognitives.com/mann-e)
  * [End-to-end Trained CNN Encode-Decoder Networks for Image Steganography](https://arxiv.org/abs/1711.07201)

#### 🔎 Detection 🔎

  * [stylegan3-detector](https://github.com/NVlabs/stylegan3-detector): StyleGAN3 Synthetic Image Detection. [![stars](https://badgen.net/github/stars/NVlabs/stylegan3-detector)](https://github.com/NVlabs/stylegan3-detector)
  * [stylegan2-projecting-images](https://github.com/woctezuma/stylegan2-projecting-images): Projecting images to latent space with StyleGAN2. [![stars](https://badgen.net/github/stars/woctezuma/stylegan2-projecting-images)](https://github.com/woctezuma/stylegan2-projecting-images)
  * [FALdetector](https://github.com/PeterWang512/FALdetector): Detecting Photoshopped Faces by Scripting Photoshop. [![stars](https://badgen.net/github/stars/PeterWang512/FALdetector)](https://github.com/PeterWang512/FALdetector)

### 🎥 Video 🎥

#### 🛠️ Tools 🛠️

  * [DeepFaceLab](https://github.com/iperov/DeepFaceLab): DeepFaceLab is the leading software for creating deepfakes. [![stars](https://badgen.net/github/stars/iperov/DeepFaceLab)](https://github.com/iperov/DeepFaceLab)
  * [faceswap](https://github.com/deepfakes/faceswap): Deepfakes Software For All. [![stars](https://badgen.net/github/stars/deepfakes/faceswap)](https://github.com/deepfakes/faceswap)
  * [dot](https://github.com/sensity-ai/dot): The Deepfake Offensive Toolkit. [![stars](https://badgen.net/github/stars/sensity-ai/dot)](https://github.com/sensity-ai/dot)
  * [SimSwap](https://github.com/neuralchen/SimSwap): An arbitrary face-swapping framework on images and videos with one single trained model! [![stars](https://badgen.net/github/stars/neuralchen/SimSwap)](https://github.com/neuralchen/SimSwap)
  * [faceswap-GAN](https://github.com/shaoanlu/faceswap-GAN): A denoising autoencoder + adversarial losses and attention mechanisms for face swapping. [![stars](https://badgen.net/github/stars/shaoanlu/faceswap-GAN)](https://github.com/shaoanlu/faceswap-GAN)
  * [Celeb DeepFakeForensics](https://github.com/yuezunli/celeb-deepfakeforensics): A Large-scale Challenging Dataset for DeepFake Forensics. [![stars](https://badgen.net/github/stars/yuezunli/celeb-deepfakeforensics)](https://github.com/yuezunli/celeb-deepfakeforensics)

#### 💡 Applications 💡

  * [face2face-demo](https://github.com/datitran/face2face-demo): pix2pix demo that learns from facial landmarks and translates this into a face. [![stars](https://badgen.net/github/stars/datitran/face2face-demo)](https://github.com/datitran/face2face-demo)
  * [Faceswap-Deepfake-Pytorch](https://github.com/Oldpan/Faceswap-Deepfake-Pytorch): Faceswap with Pytorch or DeepFake with Pytorch. [![stars](https://badgen.net/github/stars/Oldpan/Faceswap-Deepfake-Pytorch)](https://github.com/Oldpan/Faceswap-Deepfake-Pytorch)
  * [Point-E](https://github.com/openai/point-e): Point cloud diffusion for 3D model synthesis. [![stars](https://badgen.net/github/stars/openai/point-e)](https://github.com/openai/point-e)
  * [EGVSR](https://github.com/Thmen/EGVSR): Efficient & Generic Video Super-Resolution. [![stars](https://badgen.net/github/stars/Thmen/EGVSR)](https://github.com/Thmen/EGVSR)
  * [STIT](https://github.com/rotemtzaban/STIT): Stitch it in Time: GAN-Based Facial Editing of Real Videos. [![stars](https://badgen.net/github/stars/rotemtzaban/STIT)](https://github.com/rotemtzaban/STIT)
  * [BackgroundMattingV2](https://github.com/PeterL1n/BackgroundMattingV2): Real-Time High-Resolution Background Matting. [![stars](https://badgen.net/github/stars/PeterL1n/BackgroundMattingV2)](https://github.com/PeterL1n/BackgroundMattingV2)
  * [MODNet](https://github.com/ZHKKKe/MODNet): A Trimap-Free Portrait Matting Solution in Real Time. [![stars](https://badgen.net/github/stars/ZHKKKe/MODNet)](https://github.com/ZHKKKe/MODNet)
  * [Background-Matting](https://github.com/senguptaumd/Background-Matting): Background Matting: The World is Your Green Screen. [![stars](https://badgen.net/github/stars/senguptaumd/Background-Matting)](https://github.com/senguptaumd/Background-Matting)
  * [First Order Model](https://github.com/AliaksandrSiarohin/first-order-model): This repository contains the source code for the paper First Order Motion Model for Image Animation. [![stars](https://badgen.net/github/stars/AliaksandrSiarohin/first-order-model)](https://github.com/AliaksandrSiarohin/first-order-model)
  * [Articulated Animation](https://github.com/snap-research/articulated-animation): This repository contains the source code for the CVPR'2021 paper Motion Representations for Articulated Animation. [![stars](https://badgen.net/github/stars/snap-research/articulated-animation)](https://github.com/snap-research/articulated-animation)
  * [Real Time Person Removal](https://github.com/jasonmayes/Real-Time-Person-Removal): Removing people from complex backgrounds in real time using TensorFlow.js in the web browser. [![stars](https://badgen.net/github/stars/jasonmayes/Real-Time-Person-Removal)](https://github.com/jasonmayes/Real-Time-Person-Removal)
  * [AdaIN-style](https://github.com/xunhuang1995/AdaIN-style): Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization. [![stars](https://badgen.net/github/stars/xunhuang1995/AdaIN-style)](https://github.com/xunhuang1995/AdaIN-style)
  * [Frame Interpolation](https://github.com/google-research/frame-interpolation): Frame Interpolation for Large Motion. [![stars](https://badgen.net/github/stars/google-research/frame-interpolation)](https://github.com/google-research/frame-interpolation)
  * [Awesome-Image-Colorization](https://github.com/MarkMoHR/Awesome-Image-Colorization): 📚 A collection of Deep Learning based Image Colorization and Video Colorization papers. [![stars](https://badgen.net/github/stars/MarkMoHR/Awesome-Image-Colorization)](https://github.com/MarkMoHR/Awesome-Image-Colorization)


#### 🔎 Detection 🔎

  * [FaceForensics++](https://github.com/ondyari/FaceForensics): FaceForensics dataset. [![stars](https://badgen.net/github/stars/ondyari/FaceForensics)](https://github.com/ondyari/FaceForensics)
  * [DeepFake-Detection](https://github.com/dessa-oss/DeepFake-Detection): Towards deepfake detection that actually works. [![stars](https://badgen.net/github/stars/dessa-oss/DeepFake-Detection)](https://github.com/dessa-oss/DeepFake-Detection)
  * [fakeVideoForensics](https://github.com/bbvanexttechnologies/fakeVideoForensics): Detect deep fakes videos. [![stars](https://badgen.net/github/stars/bbvanexttechnologies/fakeVideoForensics)](https://github.com/bbvanexttechnologies/fakeVideoForensics)
  * [Deepfake-Detection](https://github.com/HongguLiu/Deepfake-Detection): The Pytorch implemention of Deepfake Detection based on Faceforensics++. [![stars](https://badgen.net/github/stars/HongguLiu/Deepfake-Detection)](https://github.com/HongguLiu/Deepfake-Detection)
  * [SeqDeepFake](https://github.com/rshaojimmy/SeqDeepFake): PyTorch code for SeqDeepFake: Detecting and Recovering Sequential DeepFake Manipulation. [![stars](https://badgen.net/github/stars/rshaojimmy/SeqDeepFake)](https://github.com/rshaojimmy/SeqDeepFake)
  * [PCL-I2G](https://github.com/jtchen0528/PCL-I2G): Unofficial Implementation: Learning Self-Consistency for Deepfake Detection. [![stars](https://badgen.net/github/stars/jtchen0528/PCL-I2G)](https://github.com/jtchen0528/PCL-I2G)
  * [Deepfake Scanner](https://github.com/deepware/deepfake-scanner): Deepfake Scanner by Deepware. [![stars](https://badgen.net/github/stars/deepware/deepfake-scanner)](https://github.com/deepware/deepfake-scanner)
  * [DFDC DeepFake Challenge](https://github.com/selimsef/dfdc_deepfake_challenge): A prize winning solution for DFDC challenge. [![stars](https://badgen.net/github/stars/selimsef/dfdc_deepfake_challenge)](https://github.com/selimsef/dfdc_deepfake_challenge) 

### 📄 Text 📄

#### 🛠️ Tools 🛠️
  * [GLM-130B](https://github.com/THUDM/GLM-130B): An Open Bilingual Pre-Trained Model. [![stars](https://badgen.net/github/stars/THUDM/GLM-130B)](https://github.com/THUDM/GLM-130B)
  * [LongtermChatExternalSources](https://github.com/daveshap/LongtermChatExternalSources): GPT-3 chatbot with long-term memory and external sources. [![stars](https://badgen.net/github/stars/daveshap/LongtermChatExternalSources)](https://github.com/daveshap/LongtermChatExternalSources)
  * [sketch](https://github.com/approximatelabs/sketch): AI code-writing assistant that understands data content. [![stars](https://badgen.net/github/stars/approximatelabs/sketch)](https://github.com/approximatelabs/sketch)
  * [LangChain](https://github.com/hwchase17/langchain): ⚡ Building applications with LLMs through composability ⚡. [![stars](https://badgen.net/github/stars/hwchase17/langchain)](https://github.com/hwchase17/langchain)
  * [ChatGPT Wrapper](https://github.com/mmabrouk/chatgpt-wrapper): API for interacting with ChatGPT using Python and from Shell. [![stars](https://badgen.net/github/stars/mmabrouk/chatgpt-wrapper)](https://github.com/mmabrouk/chatgpt-wrapper) 
  * [openai-python](https://github.com/openai/openai-python): The OpenAI Python library provides convenient access to the OpenAI API from applications written in the Python language. [![stars](https://badgen.net/github/stars/openai/openai-python)](https://github.com/openai/openai-python)
  * [Beto](https://github.com/dccuchile/beto): Spanish version of the BERT model. [![stars](https://badgen.net/github/stars/dccuchile/beto)](https://github.com/dccuchile/beto)
  * [GPT-Code-Clippy](https://github.com/CodedotAl/gpt-code-clippy): GPT-Code-Clippy (GPT-CC) is an open source version of GitHub Copilot, a language model -- based on GPT-3, called GPT-Codex. [![stars](https://badgen.net/github/stars/CodedotAl/gpt-code-clippy)](https://github.com/CodedotAl/gpt-code-clippy)
  * [GPT Neo](https://github.com/EleutherAI/gpt-neo): An implementation of model parallel GPT-2 and GPT-3-style models using the mesh-tensorflow library. [![stars](https://badgen.net/github/stars/EleutherAI/gpt-neo)](https://github.com/EleutherAI/gpt-neo)
  * [ctrl](https://github.com/salesforce/ctrl): Conditional Transformer Language Model for Controllable Generation. [![stars](https://badgen.net/github/stars/salesforce/ctrl)](https://github.com/salesforce/ctrl)
  * [Llama](https://github.com/facebookresearch/llama): Inference code for LLaMA models. [![stars](https://badgen.net/github/stars/facebookresearch/llama)](https://github.com/facebookresearch/llama)
  * [UL2 20B](https://ai.googleblog.com/2022/10/ul2-20b-open-source-unified-language.html): An Open Source Unified Language Learner

#### 🔎 Detection 🔎

  * [Detecting Fake Text](https://github.com/HendrikStrobelt/detecting-fake-text): Giant Language Model Test Room. [![stars](https://badgen.net/github/stars/HendrikStrobelt/detecting-fake-text)](https://github.com/HendrikStrobelt/detecting-fake-text)
  * [Grover](https://github.com/rowanz/grover): Code for Defending Against Neural Fake News. [![stars](https://badgen.net/github/stars/rowanz/grover)](https://github.com/rowanz/grover)
  * [New AI classifier for indicating AI-written text](https://openai.com/blog/new-ai-classifier-for-indicating-ai-written-text/)
  * [Discover the 4 Magical Methods to Detect AI-Generated Text (including ChatGPT)](https://medium.com/@itamargolan/uncover-the-four-enchanted-ways-to-identify-ai-generated-text-including-chatgpts-4764847fd609)
  * [GPTZero](https://gptzero.me)
  * [A Watermark for Large Language Models](https://arxiv.org/abs/2301.10226)

#### 💡 Applications 💡

  * [handwrite](https://github.com/builtree/handwrite): Handwrite generates a custom font based on your handwriting sample. [![stars](https://badgen.net/github/stars/builtree/handwrite)](https://github.com/builtree/handwrite)
  * [GPT Sandbox](https://github.com/shreyashankar/gpt3-sandbox): The goal of this project is to enable users to create cool web demos using the newly released OpenAI GPT-3 API with just a few lines of Python. [![stars](https://badgen.net/github/stars/shreyashankar/gpt3-sandbox)](https://github.com/shreyashankar/gpt3-sandbox)
  * [PassGAN](https://github.com/brannondorsey/PassGAN): A Deep Learning Approach for Password Guessing. [![stars](https://badgen.net/github/stars/brannondorsey/PassGAN)](https://github.com/brannondorsey/PassGAN)
  * [GPT Index](https://github.com/jerryjliu/gpt_index): GPT Index is a project consisting of a set of data structures designed to make it easier to use large external knowledge bases with LLMs. [![stars](https://badgen.net/github/stars/jerryjliu/gpt_index)](https://github.com/jerryjliu/gpt_index)
  * [nanoGPT](https://github.com/karpathy/nanoGPT): The simplest, fastest repository for training/finetuning medium-sized GPTs. [![stars](https://badgen.net/github/stars/karpathy/nanoGPT)](https://github.com/karpathy/nanoGPT)
  * [whatsapp-gpt](https://github.com/danielgross/whatsapp-gpt) [![stars](https://badgen.net/github/stars/danielgross/whatsapp-gpt)](https://github.com/danielgross/whatsapp-gpt)
  * [ChatGPT Chrome Extension](https://github.com/gragland/chatgpt-chrome-extension): A ChatGPT Chrome extension. Integrates ChatGPT into every text box on the internet.
  * [Unilm](https://github.com/microsoft/unilm): Large-scale Self-supervised Pre-training Across Tasks, Languages, and Modalities. [![stars](https://badgen.net/github/stars/microsoft/unilm)](https://github.com/microsoft/unilm)
  * [minGPT](https://github.com/karpathy/minGPT): A minimal PyTorch re-implementation of the OpenAI GPT (Generative Pretrained Transformer) training. [![stars](https://badgen.net/github/stars/karpathy/minGPT)](https://github.com/karpathy/minGPT)
  * [CodeGeeX](https://github.com/THUDM/CodeGeeX): An Open Multilingual Code Generation Model. [![stars](https://badgen.net/github/stars/THUDM/CodeGeeX)](https://github.com/THUDM/CodeGeeX)
  * [OpenAI Cookbook](https://github.com/openai/openai-cookbook): Examples and guides for using the OpenAI API. [![stars](https://badgen.net/github/stars/openai/openai-cookbook)](https://github.com/openai/openai-cookbook)
  * [🧠 Awesome ChatGPT Prompts](https://github.com/f/awesome-chatgpt-prompts): This repo includes ChatGPT prompt curation to use ChatGPT better. [![stars](https://badgen.net/github/stars/f/awesome-chatgpt-prompts)](https://github.com/f/awesome-chatgpt-prompts)
  * [Alice](https://github.com/greshake/Alice): Giving ChatGPT access to a real terminal. [![stars](https://badgen.net/github/stars/greshake/Alice)](https://github.com/greshake/Alice)
  * [Security Code Review With ChatGPT](https://research.nccgroup.com/2023/02/09/security-code-review-with-chatgpt)
  * [Do Users Write More Insecure Code with AI Assistants?](https://arxiv.org/abs/2211.03622)
  * [Bypassing Gmail's spam filters with ChatGPT](https://neelc.org/posts/chatgpt-gmail-spam)
  * [Recurrent GANs Password Cracker For IoT Password Security Enhancement](https://www.mdpi.com/1999-4893/15/5/155)

### 📚 Misc 📚

  * [🚀 Awesome Reinforcement Learning for Cyber Security](https://github.com/Limmen/awesome-rl-for-cybersecurity): A curated list of resources dedicated to reinforcement learning applied to cyber security. [![stars](https://badgen.net/github/stars/Limmen/awesome-rl-for-cybersecurity)](https://github.com/Limmen/awesome-rl-for-cybersecurity)
  * [Awesome Machine Learning for Cyber Security](https://github.com/jivoi/awesome-ml-for-cybersecurity): A curated list of amazingly awesome tools and resources related to the use of machine learning for cyber security. [![stars](https://badgen.net/github/stars/jivoi/awesome-ml-for-cybersecurity)](https://github.com/jivoi/awesome-ml-for-cybersecurity)
  * [Hugging Face Diffusion Models Course](https://github.com/huggingface/diffusion-models-class): Materials for the Hugging Face Diffusion Models Course. [![stars](https://badgen.net/github/stars/huggingface/diffusion-models-class)](https://github.com/huggingface/diffusion-models-class)
  * [Awesome-AI-Security](https://github.com/DeepSpaceHarbor/Awesome-AI-Security): A curated list of AI security resources. [![stars](https://badgen.net/github/stars/DeepSpaceHarbor/Awesome-AI-Security)](https://github.com/DeepSpaceHarbor/Awesome-AI-Security)
  * [ML for Hackers](https://github.com/johnmyleswhite/ML_for_Hackers): Code accompanying the book "Machine Learning for Hackers". [![stars](https://badgen.net/github/stars/johnmyleswhite/ML_for_Hackers)](https://github.com/johnmyleswhite/ML_for_Hackers)
  * [NIST AI Risk Management Framework Playbook](https://pages.nist.gov/AIRMF) 
  * [SoK: Explainable Machine Learning for Computer Security Applications](https://arxiv.org/abs/2208.10605)
  * [Who Evaluates the Evaluators? On Automatic Metrics for Assessing AI-based Offensive Code Generators](https://arxiv.org/abs/2212.06008)
  * [Vulnerability Prioritization: An Offensive Security Approach](https://arxiv.org/abs/2206.11182)
  * [MITRE ATLAS™](https://atlas.mitre.org) (Adversarial Threat Landscape for Artificial-Intelligence Systems)
  * [A Survey on Reinforcement Learning Security with Application to Autonomous Driving](https://arxiv.org/abs/2212.06123)
  * [A curated list of AI Security & Privacy events](https://github.com/ZhengyuZhao/AI-Security-and-Privacy-Events)

## 📊 Surveys 📊

  * [The Threat of Offensive AI to Organizations](https://arxiv.org/abs/2106.15764)
  * [Artificial Intelligence in the Cyber Domain: Offense and Defense](https://www.mdpi.com/2073-8994/12/3/410)
  * [A survey on adversarial attacks and defences](https://ietresearch.onlinelibrary.wiley.com/doi/10.1049/cit2.12028)
  * [Adversarial Deep Learning: A Survey on Adversarial Attacks and Defense Mechanisms on Image Classification](https://ieeexplore.ieee.org/document/9895425)
  * [A Survey of Privacy Attacks in Machine Learning](https://arxiv.org/abs/2007.07646)
  * [Towards Security Threats of Deep Learning Systems: A Survey](https://arxiv.org/abs/1911.12562)
  * [A Survey on Security Threats and Defensive Techniques of Machine Learning: A Data Driven View](https://ieeexplore.ieee.org/document/8290925)
  * [SoK: Security and Privacy in Machine Learning](https://ieeexplore.ieee.org/document/8406613)
  * [Adversarial Machine Learning: The Rise in AI-Enabled Crime and its Role in Spam Filter Evasion](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=4155496)
  * [Threats, Vulnerabilities, and Controls of Machine Learning Based Systems: A Survey and Taxonomy](https://arxiv.org/abs/2301.07474)
  * [Adversarial Attacks and Defences: A Survey](https://arxiv.org/pdf/1810.00069.pdf)
  * [Security Matters: A Survey on Adversarial Machine Learning](https://arxiv.org/abs/1810.07339)
  * [A Survey on Adversarial Attacks for Malware Analysis](https://arxiv.org/pdf/2111.08223.pdf)
  * [Adversarial Machine Learning in Image Classification: A Survey Towards the Defender’s Perspective](https://arxiv.org/pdf/2009.03728.pdf)
  * [A Survey of Robust Adversarial Training in Pattern Recognition: Fundamental, Theory, and Methodologies](https://arxiv.org/abs/2203.14046)

## 🗣 Contributors 🗣

<table>
  <tr>
    <td align="center"><a href="https://github.com/Miguel000"><img src="https://avatars2.githubusercontent.com/u/13256426?s=460&v=4" width="150;" alt=""/><br /><sub><b>Miguel Hernández</b></sub></a></td>
    <td align="center"><a href="https://github.com/jiep"><img src="https://avatars2.githubusercontent.com/u/414463?s=460&v=4" width="150px;" alt=""/><br /><sub><b>José Ignacio Escribano</b></sub></a></td>
  </tr>
</table>

## ©️ License ©️

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)

* [Creative Commons Attribution Share Alike 4.0 International](LICENSE.txt)
