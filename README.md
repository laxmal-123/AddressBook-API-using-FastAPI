# AddressBook-API-using-FastAPI
AddressBook API




from fastapi import FastAPI
from typing import Union
from pydantic import BaseModel , Field
from datetime import date


user_db={"rohan":{"username":"rohan","longitude":74.217934, "latitude":27.023804},"rohit":{"username":"rohit","longitude":19.751480, "latitude":75.713890}}
class User(BaseModel):
    username:str
    longitude:int
    latitude:int

addressBook=FastAPI()

@addressBook.get('/users')
def get_users():
    user_list=list(user_db.values())
    return user_list

@addressBook.get('/users/{username}')
def get_user_path(username:str):
    return user_db[username]

@addressBook.post('/users')
def create_user(user:User):
    username=user.username
    user_db[username]=user.dict()
    return {f'successfully create user:{username}'}

@addressBook.delete('/users/{username}')
def delete_user(username:str):
    del user_db[username]
    return {f'successfully deleted user:{username}'}   

@addressBook.put('/users')
def update_user(user:User):
    username=user.username
    user_db[username]=user.dict()
    return {f'successfully update user:{username}'}    

