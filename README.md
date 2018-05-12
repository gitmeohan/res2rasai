# res2rasai

git clone https://github.com/RasaHQ/rasa_core.git [download rasa-core and store in decision bot folder]
cd rasa_core
pip install -r requirements.txt
pip install -e .

edit port from 5005 to 5005 in the following file
C:\Users\Sohan Nipunage\Dropbox\eclipse-workspace\rasa\Decision Maker Bot\rasa_core\rasa_core\server.py

download rasa_nlu or use prepackaged in decisionmakerbot folder "git clone https://github.com/RasaHQ/rasa_nlu.git" 
pip install rasa_nlu[spacy]
python -m spacy download en_core_web_md
start cmd in admin or sudo and then run:
python -m spacy link en_core_web_md en
pip uninstall rasa_nlu

cd rasa_nlu
pip install -r requirements.txt
pip install -e .

#for new training, delete model folder and out.log for retraining.

python -m rasa_nlu.train -c nlu_model_config.json --fixed_model_name current
python3 -m rasa_nlu.train -c nlu_model_config.json --fixed_model_name current


python -m rasa_core.train -s data/stories.md -d domain.yml -o models/dialogue --epochs 300

python -m rasa_core.run -d models/dialogue -u models/nlu/default/current

pip install pypiwin32 //One-time

python -m rasa_core.server -d models/dialogue -u models/nlu/default/current -o out.log --cors *