---
title: "HashTable: 완주하지 못한 선수"
categories:
  - Post Formats
tags:
  - javascript
  - algorithm
  - hashtable
toc: true
toc_label: "Unique Title"
toc_icon: "heart"
---


### 문제설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한사항
* 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
* completion의 길이는 participant의 길이보다 1 작습니다.
* 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
* 참가자 중에는 동명이인이 있을 수 있습니다.

### 입출력 예
|participant|completion|return|
|:-------:|:-------:|:-------:|
| [leo, kiki, eden] | [eden, kiki] | leo|
| [marina, josipa, nikola, vinko, filipa] | [josipa, filipa, marina, nikola] | vinko |
| [mislav, stanko, mislav, ana] | [stanko, ana, mislav] | mislav |
{: rules="groups"}

### 코드 입력
```javascript
function solution(participant, completion) {
    var answer = '';
    // 해쉬테이블에 participant 입력 key: name, value: false
    // 해쉬테이블에 입력 key: name, value: true
    let hashTable = new HashTable();
    
    for(let i=0 ; i<participant.length ; i++){
        hashTable.set(participant[i],false);
    }
    // participant를 넣어서 false인 key값 찾기 get()이용
    for(let i=0 ; i<completion.length ; i++){
        hashTable.modify(completion[i],true);
    }
    for(let i=0 ; i<participant.length ; i++){
        if(!hashTable.get(participant[i])) answer = participant[i];
        // 동명이인에 대한 처리를 해줘야한다.
    }
    return answer;
}

class HashTable{
    constructor(size = 100000){
        this.buckets = new Array(size);
        this.size = size;
    }
    hash(key){
        let hashcode = 0;
        for(let i=0 ; i<key.length ; i++){
            hashcode += key.charCodeAt(i);
        }
        return hashcode % this.size;
    }
    set(key, value){
        let index = this.hash(key);
        // 없으면 만들고
        if(!this.buckets[index]){
            this.buckets[index]=[];
        }
        this.buckets[index].push([key, value]);
        return index;        
    }
    //이미 존재하는 값 수정
    modify(key, value){
        let index = this.hash(key);
        
        for(let buckets of this.buckets[index]){
            if(buckets[0] === key && !buckets[1]){
                buckets[1] = value;
                break;
            }
        }
    }
    
    get(key){
        let Namelist =[];
        let output=true;
        let index = this.hash(key);
        if(!this.buckets[index]) return null;
        
        for(let buckets of this.buckets[index]){    
            if(buckets[0] === key){
                Namelist.push(buckets[1]);
            }
        }
        Namelist.forEach(function(ele){
            if(ele===false) output = false;
        });
        
        return output;
    }
}
```