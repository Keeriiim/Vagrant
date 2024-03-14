## Bash
skill = "DevOps"
NUM = 123  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/80c079e7-802a-43d9-8c26-1dcc0a1ba7b3)


## Python  
#Tuple
tools = ("jenkins","terraform","docker","k8s")
print("Tuple:")
print(tools)

#Lists []
tools = ["jenkins","terraform","docker","k8s"]
print("List:")
print(tools)

#Dictionary {}
devops={"skill":"DevOps","Year":2024,"Tech":""}
print("Dictionary:")
print(devops)

print()  
#Slicing  
print("** Slicing **")  
#Get last position, increase the negative number to find starting backwards.  
print("Last position: " + str(tools[-1]))  
#Get values starting from index 2: ending position 4 (position is always located +1)  
print("Slicing 2:3: " + str(tools[2:3]))  
#Get values starting from index 2: ending position 4, then get the ket at index value 0, then get the char at index 3  
print("Slicing 2:3:0:3 : " + str(tools[2:4][0][3]))  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/7eede2ea-960b-4281-b0e1-b190235fb827)  

## JSON & YAML  
Json and Yaml are both based on python data structures.  

**JSON**  - Remove devops so that it starts and ends with {}  [JsonEditor](https://jsoneditoronline.org/)
```
{
    "skill":"DevOps",
    "Year":2024,
    "Tech":
        {
        "Cloud":"AWS",
        "Containers":"K8s",
        "CICD":"Jenkins",
        "Gitops":
            [
            "Gitlab",
            "ArgoCD",
            "Tektron"
            ]
        }
}
```  
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/8b31847e-b4d8-4a23-8484-7ffdfaa848ef)  

**Yaml**  - Change = to : after devops, then remove all {} [] "" and , then add - before all values in a List [YamlEditor](https://codebeautify.org/yaml-editor-online)  
```
Devops:
    skill: DevOps
    Year: 2024
    Tech:
        Cloud: AWS
        Containers: K8s
        CICD": Jenkins
        Gitops:
            - Gitlab
            - ArgoCD
            - Tektron
```
![image](https://github.com/Keeriiim/Vagrant/assets/117115289/3ddf3719-35b1-4f32-9901-651876b56353)



