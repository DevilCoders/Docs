## Installation

Install deps:
```bash
ansible-galaxy install -f -r requirements.yml
pip install deepdiff  # for ansible-qloud plugin
```

Deploy production
```bash
QLOUD_TOKEN=*** ansible-playbook --extra-vars="@./vars/production_variables.yml" production_playbook.yml
```

Deploy test
```bash
QLOUD_TOKEN=*** ansible-playbook --extra-vars="@./vars/test_variables.yml" test_playbook.yml
```
