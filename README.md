# HOA8.1
Hands-on Activity 8.1: Playbook for Extracting an Executable from PCAP
Testing the Github Connection
Miss na kita
Iloveyou
Wag ka papagutom
Miss u


---
- hosts: all
  gather_facts: true
  become: yes
  become_user: root

  tasks:
    - name: Collect PCAP file from server
      fetch:
        src: /home/janssenvalencia/Documents/HOA8.1Wireshark/pingPcapFile.pcap
        dest: /home/janssenvalencia/HOA8.1/PCAPDESTINATION/
        flat: yes

- hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - name: Extract executable from PCAP file
      command: "tcpflow -r /home/janssenvalencia/HOA8.1/PCAPDESTINATION/pingPcapFile.pcap -o /home/janssenvalencia/HOA8.1/pcapextracted/"
      args:
        creates: /home/janssenvalencia/HOA8.1/pcapextracted/executable.exe
    - name: Debug .exe file
      command: "cat /home/janssenvalencia/HOA8.1/report.xml"
      register: cat_output
      changed_when: false

    - debug:
        var: cat_output.stdout_lines
