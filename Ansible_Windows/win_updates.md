---
- name: UnInstalling Apache MSI
  hosts: win
  tasks:
    - name: Change power plan to high performance
      community.windows.win_power_plan:
        name: Alto desempenho

    - name: Choose which Windows updates to install
      win_updates:
        category_names:
        - SecurityUpdates
        - CriticalUpdates
        - UpdateRollups
        - Updates
        - DefinitionUpdates
        state: installed
        log_path: C:\ansible.txt
      register: result

    - debug: var=result

    - win_reboot:
      when: result.reboot_required
