import json

from difflib import get_close_matches 



def load_knowledge(file_path:str) -> dict:
    with open(file_path,'r') as file:
        data: dict =json.load(file)
        return data
    

def save_knowledge(file_path: str, data: dict):
    with open(file_path, 'w') as file:
        json.dump(data, file, indent=2) 




def find_best_match(user_question:str,question:list[str])->str|None:
    matches:list=get_close_matches(user_question,question,n=1,cutoff=0.7)
    return matches[0] if matches else None


def get_answer_for_question(question:str,knowledge:dict)->str|None:
    for q in knowledge["questions"]:
        if q["questions"]==question:
            return q["answer"]


def chat_bot():
    knowledge: dict=load_knowledge('knowledge.json')

    while True:
        user_input:str=input("you: ")

        if user_input.lower()=="quit":
            break


        best_match:str|None=find_best_match(user_input,[q["questions"] for q in knowledge["questions"]])


        if best_match:
            answer:str=get_answer_for_question(best_match,knowledge)
            print(f"Bot:{answer}")
        else:
            print("Bot : I do not know the answer can you teach me?")
            new_answer:str=input('type the new answer or "skip" to skip:')
            if new_answer.lower!='skip':
                knowledge["questions"].append({"questions":user_input,"answer":new_answer}) 
                save_knowledge('knowledge.json',knowledge)
                print("Bot : thank you i learn a new response")







if __name__ == '__main__':
    chat_bot()

