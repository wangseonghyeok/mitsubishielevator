# Introduction
웹사이트 반응형 페이지
* Component Language : Html,css,JavaScript,
* design : Photoshop

# Description
메인페이지,서브페이지(GNB : Products Quickmenu : project)이동경로 한국지사 미쓰비시엘레베이터 구축 홈페이지입니다.

# Creation Period
2022-08-07 ~ 08-15
# finished version
![PC_main_01_수정](https://user-images.githubusercontent.com/102776957/191402937-982c2d1b-92ca-48ac-9bf8-e38ee3dc8f28.jpg)

# Features
* Swiper
* Axios

# Development(Main Page Important part)
![1](https://user-images.githubusercontent.com/102776957/191398513-9ff3d865-51f1-4d5e-8375-07d4bfac7b3b.JPG)
* 숫자 애니메이션을 구현  division loadCapacity doubleDech
  * 함수 조건을 1000단위로 콤마(,),새로운 문자열로 대체,새로운 문자열 반환 replace 메소드
  * /\B(?=(\d{3})+(?!\d) = \B = 문자 존재,\d{3} = 문자열 3글자,?!\d = 문자열 3글자 초과x
* division(Math.round(this.val)) 함수를 받은 입력값을 정수 값으로 반환
* 스크롤 scrollY 360이상 일때 함수 실행!
```C
      const memberCountMetor = 1230;
      const memberCountKg = 5250;
      const memberCountDouble = 2;
      let minSpeed = $(".wrap .minSpeed");
      minSpeed.html(`0<span>m</span>`);

      let minWeight = $(".wrap .minweight");
      minWeight.html(`0<span>kg</span>`);

      let minNumber = $(".wrap .minNumber");
      minNumber.html(`0<span>(Double)</span>`);

      let superFast = function () {
        $({ val: 0 }).animate(
          { val: memberCountMetor },
          {
            duration: 2000,
            step: function () {
              const meter = 
              * division(Math.round(this.val));
              minSpeed.html(`${meter}<span>m</span>`);
            },
            complete: function () {
              const meter = division(Math.round(this.val));
              minSpeed.html(`${meter}<span>m</span>`);
            },
          }
        );
      };
      let superWeight = function () {
        $({ val: 0 }).animate(
          { val: memberCountKg },
          {
            duration: 2000,
            step: function () {
              const meter = loadCapacity(Math.round(this.val));
              minWeight.html(`${meter}<span>m</span>`);
            },
            complete: function () {
              const meter = loadCapacity(Math.round(this.val));
              minWeight.html(`${meter}<span>m</span>`);
            },
          }
        );
      };
      let superNumber = function () {
        $({ val: 0 }).animate(
          { val: memberCountDouble },
          {
            duration: 2000,
            step: function () {
              const meter = doubleDech(Math.round(this.val));
              minNumber.html(`${meter}<span>(Double)</span>`);
            },
            complete: function () {
              const meter = doubleDech(Math.round(this.val));
              minNumber.html(`${meter}<span>(Double)</span>`);
            },
          }
        );
      };
      
      function division(x) {
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      }
      function loadCapacity(x) {
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      }
      function doubleDech(x) {
        return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
      }
      
       $(window).on("scroll", function (event) {
        const scrollY = $(window).scrollTop();
        // console.log(scrollY);
        if (scrollY >= 350) {
          superFast(); 
          superWeight();
          superNumber();
          $(this).off(event);
        }
      });
 ```
 # Development(Sub Page mportant part)
![5](https://user-images.githubusercontent.com/102776957/191399556-2ad2ea94-5a0d-48e2-afa2-73f57ebc845c.JPG)
* 용도별 엘레베이터 종류 조건 
  * speed,category (제이슨파일로 데이터를 넣었다..)

![4](https://user-images.githubusercontent.com/102776957/191399640-3a1b6fd2-2e5a-4e4c-96bd-268319292544.JPG)

* 조건 : 초고속 : 360, 이상 고속 : 120~359, 중저속 : 나머지
```C
    const speedMatch = (value) => {
      if (value >= 360) return "superfast";
      else if (value >= 120 && value < 360) return "fast";
      else return "low";
    };
```

* 조건 : 용도별 오피스,호텔,주상복합,아파트,공공병원,MOD
  * input data-filter속성값 : let chkboxes = document.querySelectorAll("[data-filter]");
   
```C
          if (Object.keys(target.dataset)[0] == "filter") {
          // 용도 박스는 1개만 선택된다.
          chkboxes.forEach((itm) => {
            if (itm.dataset.filter != target.dataset.filter) itm.checked = false;
          });
          if (Array.from(chkboxes).filter((itm) => itm.checked).length == 0) {
            if (speedArray.length == 0) filteredData = allData;
            else if (speedArray.length > 0) filteredData = allData.filter((itm) => speedArray.includes(itm.speedStandard));
          } else {
            if (speedArray.length == 0) filteredData = allData.filter((itm) => itm.category == target.dataset.filter);
            else if (speedArray.length > 0) filteredData = allData.filter((itm) => itm.category == target.dataset.filter).filter((itm) => speedArray.includes(itm.speedStandard));
          }
        } else if (Object.keys(target.dataset)[0] == "speedfilter") {
          // 속도 박스는 여러 개 선택 가능
          speedArray = Array.from(speedBoxes)
            .filter((itm) => itm.checked)
            .map((itm) => itm.dataset.speedfilter);

          let checkedValue = Array.from(chkboxes)
            .filter((itm) => itm.checked)
            .map((itm) => itm.dataset.filter)[0];
