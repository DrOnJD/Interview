# JS
  1.  ## Рассказать про контекст/this
      #### Задачa
        Что выведется в консоли?
        ```js
        const object = {
          regular: function() {
              console.log(this);
          },
          arrow: () => {
            console.log(this);
          }
        };
        const assignedRegular = object.regular;

        object.regular();
        object.arrow();
        assignedRegular();
        ```

      #### Ответ
      ```js
      ({ regular: f, array: f })
      (Window {...})
      (Window {...})
      ```

        * ### Как можно передать/назначить контекст
          #### Задача
          Что выведется в консоли?
          ```js
          const object = {
            regular: function(...args) {
              console.log(this, ...args);
            },
            arrow: (...args) => {
              console.log(this, ...args);
            },
          };

          object.regular.call(window.location, [1, 2, 3]);
          object.regular.bind(window.location, [1, 2, 3])();
          object.arrow.call(window.location, [1, 2, 3]);
          object.arrow.bind(window.location, [1, 2, 3])();
          ```

          #### Ответ
            ```js
            (Location {...}, [1, 2, 3])
            (Location {...}, 1, 2, 3)
            (Window {...}, [1, 2, 3])
            (Window {...}, 1, 2, 3)
            ```


  2.  ## Замыкания
      Расскажи что знаешь о замыканиях

      #### Задача
      Перечисли как можно больше вариантов решения задачи
      ```js
      for (var i = 0; i < 10; i++) {
        setTimeout(() => console.log(i), 50);
      };
      ```

      #### Ответ
      ```js
      for (var i = 0; i < 10; i++) {
        (() => {
            let j = i;
            setTimeout(() => console.log(j), 50);
        })();
      };

      for (var i = 0; i < 10; i++) {
        ((i) => {
          setTimeout(() => console.log(i), 50);
        })(i);
      };

      for (var i = 0; i < 10; i++) {
        setTimeout((i) => console.log(i), 50, i);
      };

      for (let i = 0; i < 10; i++) {
        setTimeout(() => console.log(i), 50);
      };
      ```


  3.  ## Расскажи про эвентлуп
      *  Call stack - Стек вызовов
      *  Web api - Браузерное апи, реализует асинхронность
      *  Callback queue - очередь задач возвращенных из web api
      *  Event loop - механизм добавляющий задачи из callback queue в call stack при освобождении последнего
      *  Tick - момент освобождения call stack от задач

  4.  ## Расскажи про асинхронность в JS
      * JS синхронный или асинхронный язык (однопоточный/многопоточный)
      * Расскажи про промисы
        * Что возвращают промисы
        * Статусы промисов
          * pending
          * fulfilled
          * rejected
        * Как обрабатывать ошибки промисов
      * Что выведет код
        #### Задача
        ```js
        const promise = new Promise((res) => {
          console.log(1); // порядок - х, значение - у
          return res(2);
        }).then((j) => console.log(j)); // порядок - х, значение - у

        setTimeout(() => console.log(3), 0); // порядок - х, значение - у

        promise.then(console.log); // порядок - х, значение - у

        const func = () => console.log(4); // порядок - х, значение - у

        func();
        ```

        #### Ответ
        ```js
        1
        4
        2
        undefined
        3
        ```
      * Что выведет код
        #### Задача
        ```js
        Promise
          .resolve(1)
          .then((res) => {
              console.log('then 1: ', res); //
              return res * x;
          })
          .then((res) => {
              console.log('then 2: ', res); //
              return res / 2;
          })
          .catch((res) => {
              console.log('catch', res); //
              return 4;
          })
          .then((res) => {
              console.log('then 3: ', res); //
              return res / 4;
          })
          .finally((res) => {
              console.log('finally:', res); //
          });
        ```

        #### Ответ
        ```js
        (then 1:  1)
        (Error: x is not defined)
        (then 3:  4)
        (finally: undefined)
        ```

  5.  ## Расскажи про нововведения JS ES6 и более поздних
      * Спред оператор
        * Диструктуризация
        * Rest параметры
        * Конкатенация массивов и объектов
      * Шаблонные строки
      * Optional chaining
      * `Promise`
        * `.all`
        * `.any`
        * `.allSettled`
      * `async/await`
      * `Map/Set`
      * Запись чисел через сепоратор `1_234_500`
      * Классы
        * `private` свойства
        * `private` аксессоры
        * `static` свойства
      * Массивы
        * `for_of`, `for_in`
        * `.toReversed`
        * `.toSorted`
        * `.toSpliced`
        * `.with`
      * Особенности стрелочных функций
        * Удобнее запись
        * Не обладают своим контекстом
        * Наследуют контекст из внешней области видимости
        * Невозможно назначить контекст с помощью `bind`, `call`, `apply`
        * Не могут быть конструктором
        * Отсутствует аргумент `arguments`
      * let/const
        * `let` При использовании в цикле, для каждой итерации создаётся своя переменная.
        * `const` Создает константу, значение которой нельзя поменять
        * `let/const` Имеет блочную видимость
        * `let/const` Переменная не доступна до объявления (не всплывает)
      * Расскажи про записи и кортежи (records/tuples)

  6.  ## Что такое Event bubbling и Event capturing?
  7.  ## Сравните методы объекта event stopPropagation и stopImmediateProparation.

# React
  1. ## В чем разница `memo` и `useMemo`?
      #### Ответ
        * `memo` - это hook для мемоизации значений
        * `useMemo` - это HOC для мемоизации компонента в зависимости от результатов каллбека
  2. ## Что такое `Lazy loading`, `Сode splitting`
      #### Ответ
        Это подходы для нарезки и загрузки только используемого кода.
  3. ## Что подразумевается под тепмином `Чистая функция`
      #### Ответ
        Для некоторого набора значений переданных в фунцию, она всегда вернет один и тот же результат. Т.е. функция в своей работе должна опираться только на переданные значения и не на что более (значения из окружения, временнЫе значения, рандомайдеры и т.д.)
  4. ## Напишите хук `useToggle`
     #### Задача
      * На выход хук долен выдавать 3 метода
        * Состояние
        * Метод тогла
        * Метод назначения конкретного значения
      * На вход хук получает дефолтное состояние
     #### Ответ
      ```js
      const useToggle = (defaultState) => {
        const [state, setState] = useState(defaultState);

        const toggle = useCallback(() => setState((a) => !a), []);

        return [state, toggle, setState];
      };
      ```
  5. ## Напишите хук `useDebounce`
      #### Задача
        * На выход хук долен выдавать значение
        * На вход хук получает значение и задержку
      #### Ответ
        ```js
        const useDebounce = (value, delay) => {
          const [state, setState] = useState(value);

          useEffect(() => {
            const timeoutId = setTimeout(setState, delay, value);
            return () => clearTimeout(timeoutId);
          }, [value, delay]);

          return state;
        };
        ```

  6. ## Какие есть проблемы в компоненте
      #### Задача
        ```js
        import React, { useEffect, useState, useCallback } from 'react';
        import { func, number, string } from 'prop-types';
        import { useSelector } from 'react-redux';
        import selectTexts from 'selectors/texts';

        import styles from './ParagraphEditor.scss';


        const themes = {
          dark: {
            color: '#FFF',
            backgroundColor: '#000',
          },
          light: {
            color: '#000',
            backgroundColor: '#FFF',
          },
        };


        const Component = ({ onClick, buttonIndex, themeName }) => {
          const selectedTexts = useSelector(selectTexts);
          const [value, setValue] = useState(0);
          const [text, setText] = useState(selectedTexts.filter((item) => item.theme === themeName)[buttonIndex]);
          const [style] = useState(themes[themeName]);

          const onChangeSelect = useCallback((e) => setValue(value + e.target.value), [value]);

          useEffect(() => setText(selectedTexts.filter((item) => item.theme === themeName)[buttonIndex]), [themeName, selectedTexts]);

          return (
            <>
              <select onChange={onChangeSelect}>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
              </select>
              <div className={styles.button} style={style} onClick={() => onClick(value)}>{text}</div>
            </>
          );
        };

        Component.propTypes = {
          onClick: func.isRequired,
          buttonIndex: number.isRequired,
          themeName: string.isRequired,
        };
        ```

      #### Ответ
        * style не обновится при изменении themeName в целом это не обязательно кешировать, а если кешировать, то через useMemo
        * Вместо setText и useEffect лучше использовать useMemo
        * При изменении buttonIndex useEffect не отработает, т.к. пропс отсутствует в зависимостях
        * В пропсах используются анонимные функции
        * При изменении селекта получим ерунду, т.к. строка складывается с числом
        * onChangeSelect не имеет смысла кешировать т.к. каллбек будет обновляться при каждом изменении value. Лучше использовать в setValue каллбек

