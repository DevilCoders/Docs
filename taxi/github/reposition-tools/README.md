# reposition-tools
Various reposition-related scripts (for visualization and other debug needs).

Install:
pip3 install -r requirements.txt

It's also required to fill ~/.reposition_nirvana_config.json in form of {"production": {"api_url": {URL}, "token": {OAUTH_TOKEN}}

Run: visualize.py --env=production --workflow_instance_id=ID --block_guid=ID
