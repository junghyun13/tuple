# tuple
# When a string s containing a set representing a specific tuple using the properties of a tuple is given as a parameter, return the tuple represented by s in an array! 튜플의 성질을 이용해서 특정 튜플을 표현하는 집합이 담긴 문자열 s가 매개변수로 주어질 때, s가 표현하는 튜플을 배열에 담아 return 해라!
# 튜플의 성질
중복된 원소가 있을 수 있습니다. ex : (2, 3, 1, 2)
원소에 정해진 순서가 있으며, 원소의 순서가 다르면 서로 다른 튜플입니다. ex : (1, 2, 3) ≠ (1, 3, 2)
튜플의 원소 개수는 유한합니다.
# python
# case 1:
import re
def solution(s):
    answer=[]
    a=s.split(',{')
    a.sort(key=len)
    for j in a:
        numbers = re.findall("\d+", j) #findall메소드는 정규식과 매치되는 모든 문자열을 리스트로 돌려준다.--> 숫자에 해당한다면 리스트로 돌려줌
        for k in numbers:
            if int(k) not in answer:
                answer.append(int(k))
    return answer
s="{{2},{2,1},{2,1,3},{2,1,3,4}}"
print(solution(s))
# case 2:
def solution(s):
    s = Counter(re.findall('\d+', s))
    return list(map(int, [k for k, v in sorted(s.items(), key=lambda x: x[1], reverse=True)]))
import re
from collections import Counter
#case 3:
def solution(s):
    answer = []
    s1 = s.lstrip('{').rstrip('}').split('},{')
    new_s = []
    for i in s1:
        new_s.append(i.split(','))
    new_s.sort(key = len)
    for i in new_s:
        for j in range(len(i)):
            if int(i[j]) not in answer:
                answer.append(int(i[j]))
    return answer
#result--> [2, 1, 3, 4]
