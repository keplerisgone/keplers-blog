---
{"dg-publish":true,"permalink":"/02-Area/CS-CA-SW/(CS-CA-SW) Structure of commands/","tags":["Area/CS-CA-SW"],"noteIcon":"","created":"2025-01-05T15:55:09.000+09:00","updated":"2025-04-07T22:55:10.013+09:00"}
---

# Structure of commands

## 명령어의 구조

명령어는 크게 연산 코드(`operation code`)와 오퍼랜드(`operand`)로 구성되어 있습니다. 연산 코드를 다른 말로 연산자, 오퍼랜드는 다른 말로 피연산자라고도 부르기도 합니다.

연산 코드가 담기는 영역을 연산 코드 필드(`operation code field`), 오퍼랜드가 담기는 영역을 오퍼랜드 필드(`operand field`)라고 부릅니다.

명령어는 각각의 필드에 담긴 내용을 불러와 명령을 수행합니다. 

### 오퍼랜드

오퍼랜드는 연산에 필요한 데이터이고, 오퍼랜드 필드는 오퍼랜드가 담기는 필드이기에 오퍼랜드 그 자체나 오퍼랜드가 담긴 주소값이 저장될 수 있습니다.

많은 경우에 주소값이 저장되는 경우가 대부분입니다.

명령어는 필요한 오퍼랜드의 개수에 따라 나뉠 수 있는데, 순서대로 `0-주소 명령어`, `1-주소 명령어`, `2-주소 명령어`, `3-주소 명령어`로 나뉩니다.

### 연산 코드

연산 코드의 유형은 크게 네가지로 나눌 수 있습니다.

- 데이터 전송 : 말 그대로 데이터와 관련된 명령어입니다. 메모리와 관련되어 있는 경우가 많습니다.
- 산술/논리 연산 : 연산을 수행합니다. 결과값이 있는 경우가 대부분입니다.
- 제어 흐름 변경 : 프로그램의 실행과 관련되어 있습니다.
- 입출력 제어 : 입출력 장치로부터 데이터를 가져오거나 전달합니다.

### 주소 지정 방식

그냥 오퍼랜드를 담으면 될 걸 왜 굳이 주소를 지정해서 사용할까요?

답은 *”주소를 안 쓰면 명령어에 공간이 너무 부족해서”*입니다. 명령어의 비트수는 한계가 있고, 여기에 모든 오퍼랜드를 담는 것은 무리가 있기에 
오퍼랜드를 담는 주소를 이용합니다. 주소를 사용하면 오퍼랜드의 크기는 메모리가 담을 수 있는 공간만큼 커지게 됩니다. 서랍같은 거라고 생각하면 편할까요?

이렇게 사용되는 주소를 유효 주소(`effective address`)라고 하고, 주소를 지정하는 방식을 주소 지정 방식(`addressing mode`)라고 합니다.

주소 지정 방식은 다섯 가지로 나눌 수 있습니다.

- 즉시 주소 지정 방식(`immediate addressing mode`)은 연산에 사용할 오퍼랜드를 오퍼랜드 필드에 명시하는 방식입니다. 좁습니다.
    - *연산 코드 : 데이터*
- 직접 주소 지정 방식(`direct addressing mode`)은 오퍼랜드 필드에 유효 주소를 등록하는 방식입니다. 그래도 유효 주소의 길이에 제한이 있습니다.
    - *연산 코드 : 유효 주소 → 데이터 접근*
- 간접 주소 지정 방식(`indrect addressing mode`)은 오퍼랜드 필드에 유효주소의 주소를 등록하는 방식입니다. 제한이 조금 좁아졌습니다. 근데 느립니다.
    - *연산 코드 : 유효 주소의 주소 → 유효 주소 → 데이터*

다음은 레지스터를 사용하는 방식입니다.

- 레지스터 주소 지정 방식(`register addressing mode`)은 오퍼랜드를 저장한 레지스터를 필드에 직접 명시하는 방식입니다. 메모리보다 빠릅니다. 레지스터 주소의 길이에 제한이 있습니다.
    - *연산 코드 : 유효 주소 → 레지스터*  *→ 데이터*
- 레지스터 간접 주소 방식(`register indrect addressing mode`)은 유효 주소를 저장한 레지스터를 명시하는 방식입니다. 간접 주소 지정 방식과 유사합니다.
    - *연산 코드 : 유효 주소를 저장한 레지스터 → 유효 주소 → 데이터*

### Stack and queue

스택과 큐는 가장 많이 사용하는 데이터 구조 중 하나입니다.

다음의 내용을 참고해주세요.

- Stack
    - 계층식으로 데이터를 쌓는 구조를 말합니다.
    - vector식, linked list식으로 구현할 수 있습니다.
    - vector식
    
    ```cpp
    template <class T>
    class stack{
    	private;
    		size_t top;
    		vector<T> items;
    	public:
    		stack() {}
    		push(const T&) {}
    };
    
    stack::stack(){
    	top=0;
    }
    void stack::push(const T& val){
    	items[top] = val;
    	top++;
    }
    T& stack::pop(){
    	if(empty()) throw std::out_of_range("underflow");
    	top--;
    	T& item = items[top];
    	items[top] = null;
    	return item;
    }
    T& stack::peek(){
    	if(empty()) throw std::out_of_range("underflow");
    	return items[top-1];
    }
    bool stack::empty(){
    	if (top==0) return true;
    	else return flase;
    }
    size_t stack::size() {
    	return top;
    }
    ```
    
    - linked list식
        - push할 때보면 ‘함수안에서 동적할당 해도 되는건가… 어차피 사라지지 않나’ 라고 생각할 수 있는데, 어차피 newnode포인터는 Stack에 저장되어 함수 호출이 종료되면 사라지고, 동적할당된 Node는 heap에 남게 되어 head가 이를 가리키게 됩니다.
        - 어찌보면 함수 내부에서 그냥 Node를 생성하지 않는 이유이기도 합니다.
    
    ```cpp
    template <class T>
    class stack{
    	private:
    		size_T length;
    		LinkedList<T> items;
    	public:
    		...
    }
    
    stack::stack(){
    	length = 0;
    	items.head = null;
    }
    
    void stack::push(const T& val){
    	length++;
    	Node<T> *newNode = new Node<T>(val);
    	newNode->next = head;
    	items.head = newNode;
    }
    void stack::pop(){
    	if ...
    	length--;
    	Node<T> *node = items.head; // head가 가리키는 노드를 node가 가리키게 한다
    	items.head = node->next; // node의 다음 노드가 가리키는 곳을 head가 가리키게 한다 (결국 head의 다음 다음 노드)
    	delete node;
    } // 그럼 앞의 노드가 남잖아
    T& stack::peek() {
    	if...
    	return items.head;
    }
    ```
    
- Queue
    - stack과 달리 들어온 순서대로 처리합니다.
    - 네트워크 정보 처리, 줄세우기 등에 사용합니다.
    - array ← 많이 사용합니다. ← 사이즈가 고정되어있을 때 사용
        
        ```cpp
        강의실이 전보다 한산해졌어요
        template<class T>
        class queue{
        	private:
        		size_t length, size, head, tail;
        		T* items;
        	public:
        		...
        };
        
        template<class T>
        queue::queue(size_t 1){
        	length = 1;
        	items = new T[length];
        	size = 0;
        	head = 0;
        	tail = 0;
        }
        
        template <class T>
        void queue::enqueue(const T& val){
        	if(size == length) {throw std::out_of_range("overflow");}
        	items[tail] = val;
        	tail = (tail + 1) % length;
        	size++;
        }
        
        template <class T>
        T& queue::dequeue(){ 
        	if(size == 0){throw std::out_of_range(“underflow");}
          T& item = items[head];
        	items[head] = null;
        	head = (head+1) % length;
        	size--;
          return item;
        }
        
        T& queue::peek(){ 
        	if(size == 0)
        	{throw std::out_of_range(“underflow");}
          return items[head];
        }
        
        bool queue::empty(){ if(size == 0) return true; else return false;
        }
        
        size_t queue::size(){ return size;
        }
        ```
        
        - size_t ?
        - 근데 queue하다가 tail이 오버플로우되면 어떡해요 ← head도 ← 멍청이
        - queue의 크기가 $2^n$일 경우는 (tail+)&0x($2^n-1$)으로 할 수 있다 - 더 빠르다
            - 복잡한건줄 알았는데 그냥 AND였음
                
                [[🔗 LINK\|🔗 LINK]](https://falsy.me/c-cpp-%EA%B3%B5%EB%B6%80%ED%95%98%EA%B8%B0-2-%EB%B9%84%ED%8A%B8-%EC%97%B0%EC%82%B0%EC%9E%90-%EB%B9%84%ED%8A%B8-%EC%9D%B4%EB%8F%99shift-%EC%97%B0%EC%82%B0%EC%9E%90/) — 폴시랩
                
            
    - Linked List
        
        ```cpp
        template<class T> 
        class queue{
          private:
            size_t length;
            LinkedList<T> items;
        	public: ...
        };
        
        queue::queue(){ 
        	length = 0; 
        	items.head = null;
        }
        
        void queue::enqueue(const T& val){ 
        	length++; 
        	items.push_front(val);
        }
        
        void queue::dequeue(){
        	if(empty()) {throw std::out_of_range("underflow");}
        	length--;
        	items.pop_back();
        }
        
        T& queue::peek(){
        	if(empty()) throw std::out_of_range("underflow"); 
        	return items.tail;
        }
        
        bool queue::empty(){ if(length == 0) return true; else return false;
        }
        size_t queue::size(){ return length;
        }
        ```
        
        -