# Task was to run a image captioning codebase and update the code for the Bangla dataset.
## Dataset
The dataset was given from [BanglaLekhaImageCaptions](https://data.mendeley.com/datasets/rxxch9vw59/2)
# Procedure
## Dataset preprocessing
The dataset was well prepared. So I put the data to the model directly as the git repo mentioned to train their code.
I split the data manually for 1000 images for the first train attempt.
## Updated code for given dataset
I besically updated three file for the dataset.
1. configuration.py (For data location)
2. coco.py
```
class CocoCaption(Dataset):
    def __init__(self, root, ann, max_length, limit, transform=train_transform, mode='training'):
        super().__init__()

        self.root = root
        self.transform = transform
        self.annot = [(val['filename'], val['caption'][0])
                      for val in ann]
        if mode == 'validation':
            self.annot = self.annot
        if mode == 'training':
            self.annot = self.annot[: limit]

        self.tokenizer = BertTokenizer.from_pretrained(
            'bert-base-uncased', do_lower=True)
        self.max_length = max_length + 1

    # def _process(self, image_id):
    #     val = str(image_id).zfill(12)
    #     return val + '.jpg'

    def __len__(self):
        return len(self.annot)

    def __getitem__(self, idx):
        image_id, caption = self.annot[idx]
        image = Image.open(os.path.join(self.root, image_id))

        if self.transform:
            image = self.transform(image)
        image = nested_tensor_from_tensor_list(image.unsqueeze(0))

        caption_encoded = self.tokenizer.encode_plus(
            caption, max_length=self.max_length, pad_to_max_length=True, return_attention_mask=True, return_token_type_ids=False, truncation=True)

        caption = np.array(caption_encoded['input_ids'])
        cap_mask = (
            1 - np.array(caption_encoded['attention_mask'])).astype(bool)

        return image.tensors.squeeze(0), image.mask.squeeze(0), caption, cap_mask

```
3. predict.py (Created a new version for my trained model to predict a caption)
```
elif version == 'v4':
    model,_ = caption.build_model(config)
    print("Loading Checkpoint...")
    checkpoint = torch.load('/content/catr/checkpoint.pth', map_location='cpu')
    model.load_state_dict(checkpoint['model'])
```
# Finally
I have given all three files in the repo. If you run my colab make sure that after cloning the git repo of the codebase, you have changed those three files.
