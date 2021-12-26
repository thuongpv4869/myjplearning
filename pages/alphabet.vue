<template>
  <div>
    <div>
      {{ questions.filter((q) => q.correct).length }}/{{ questions.length }}
    </div>
    <div>
      wrong:
      {{
        questions
          .filter((q) => q.showResult && !q.correct)
          .map((q) => q.question)
      }}
    </div>
    <button @click="shuffleQuestion">shuffle question</button>
    <div>
      {{ questions.indexOf(currentQuestion) + 1 }}.
      {{ currentQuestion.question }}
    </div>
    <div>
      <button @click="preQuestionHandler">previous</button>
      <input
        type="text"
        v-model="currentQuestion.userAnswer"
        @keyup.enter="userAnswerHandler"
      /><button v-on:click="userAnswerHandler">answer</button>
      <button @click="nextQuestionHandler">next</button>
    </div>
    <div v-if="currentQuestion.showResult">
      <span>{{ currentQuestion.correct ? "true" : "false" }}</span>
      <span v-if="!currentQuestion.correct">{{ currentQuestion.answer }}</span>
    </div>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "IndexPage",
  data: function () {
    return {
      searchKey: "アルファベット読み方",
      imageOriginLink:
        "https://eigodekore.com/wp-content/uploads/2016/11/38026e5b0dcf0e1b9c3a9750d41a891e.jpg",
      questions: [],
      currentQuestion: null,
      alphabet: {
        a: "エイ",
        b: "ビー",
        c: "シー",
        d: "ディー",
        e: "イー",
        f: "エフ",
        g: "ジー",
        h: "エイチ",
        i: "アイ",
        k: "ケイ",
        l: "エル",
        m: "エム",
        n: "エヌ",
        o: "オウ",
        p: "ピー",
        q: "キュー",
        r: "アール",
        s: "エス",
        t: "ティー",
        u: "ユー",
        v: "ヴィー",
        w: "ダブリュ",
        x: "エックス",
        y: "ワイ",
        z: "ズィー",
      },
      itVocab: {
        url: "",
        http: "",
        https: "",
        request: "",
        response: "",
        protocol: "",
        deploy: "",
        develop: "",
        production: "",
        staging: "",
        dev: "",
        feature: "",
        branch: "",
        git: "",
        commit: "",
        rebase: "",
        merge: "",
        "pull request": "",
        conflict: "",
        resolve: "",
        master: "",
        "CI/CD": "",
        docker: "",
        container: "",
        client: "",
        github: "",
        account: "",
        ssh: "",
        serve: "",
        bug: "",
        error: "",
        linux: "",
        window: "",
        macos: "",
        ios: "",
        iphone: "",
        android: "",
        version: "",
        control: "",
        config: "",
        file: "",
        clear: "",
        cache: "",
        database: "",
        mysql: "",
        rdbms: "",
        nosql: "",
        ai: "",
        algorithm: "",
        structure: "",
        "code base": "",
        project: "",
        clone: "",
        extension: "",
        plugin: "",
        testing: "",
        "unit test": "",
        tester: "",
        microsoft: "",
        google: "",
        search: "",
        stackoverflow: "",
        facebook: "",
        twitter: "",
        screen: "",
        comment: "",
        release: "",
        python: "",
        javascript: "",
        "c++": "",
        computer: "",
        cloud: "",
        amazone: "",
        storage: "",
        click: "",
        hover: "",
        html: "",
        css: "",
        frontend: "",
        backend: "",
        fullstack: "",
        developer: "",
        semicolon: "",
        mouse: "",
        terminal: "",
        window: "",
        chrome: "",
        edge: "",
        app: "",
        react: "",
        vue: "",
        console: "",
        ui: "",
        ux: "",
        nodejs: "",
        gitlab: "",
        jenkin: "",
        build: "",
        success: "",
        failed: "",
        string: "",
        number: "",
        dictionary: "",
        data: "",
        key: "",
        word: "",
        press: "",
        sound: "",
        card: "",
        component: "",
        object: "",
        type: "",
        api: "",
        django: "",
        translate: "",
        debug: "",
        document: "",
        desktop: "",
        folder: "",
        reset: "",
        shutdown: "",
        enter: "",
        space: "",
        ctrl: "",
        alt: "",
        shift: "",
        home: "",
        fn: "",
        tab: "",
        default: "",
        page: "",
        index: "",
        i18n: "",
        framework: "",
        library: "",
        account: "",
        brSE: "",
        pm: "",
        manager: "",
        leader: "",
        team: "",
        game: "",
        code: "",
        cpu: "",
        ram: "",
        chip: "",
        perfomance: "",
        line: "",
        refresh: "",
        estimate: "",
        function: "",
        command: "",
        statement: "",
        company: "",
        username: "",
        user: "",
        password: "",
        "forgot password": "",
        wifi: "",
        internet: "",
        connect: "",
        encode: "",
        notification: "",
        certiface: "",
        security: "",
        mode: "",
        extension: "",
        title: "",
        selector: "",
        null: "",
        array: "",
        undefined: "",
        character: "",
        boolean: "",
        integer: "",
        float: "",
        double: "",
        dynamic: "",
        static: "",
        current: "",
        datetime: "",
        day: "",
        month: "",
        year: "",
        hour: "",
        minute: "",
        second: "",
        byte: "",
        kilobyte: "",
        gigabyte: "",
        megabyte: "",
        bit: "",
        link: "",
        ref: "",
        back: "",
        button: "",
        input: "",
        compile: "",
        module: "",
        setting: "",
        tag: "",
        oop: "",
        caplock: "",
        this: "",
        readme: "",
        json: "",
        package: "",
        youtube: "",
        manga: "",
        image: "",
        screenshot: "",
        capture: "",
        record: "",
        cancel: "",
        submit: "",
        call: "",
        music: "",
        vscode: "",
        pycharm: "",
        column: "",
        row: "",
        responsive: "",
        text: "",
        color: "",
        scroll: "",
        out: "アウト",
        source: "ソース",
      },
    };
  },
  created: function () {
    this.questions = this.generateQuestion();
    this.currentQuestion = this.questions[0];
  },
  methods: {
    generateQuestion: function () {
      let _questions = [];
      for (const key in this.alphabet) {
        _questions.push({
          question: key,
          answer: this.alphabet[key],
          userAnswer: null,
          correct: false,
          showResult: false,
        });
      }
      return _questions;
    },
    shuffleQuestion: function () {
      let _questions = this.generateQuestion();
      this.questions = _.shuffle(_questions);
      this.currentQuestion = this.questions[0];
    },
    nextQuestionHandler: function () {
      const currentQuestionIndex = this.questions.indexOf(this.currentQuestion);
      if (currentQuestionIndex <= this.questions.length - 1 - 1) {
        this.currentQuestion = this.questions[currentQuestionIndex + 1];
      }
    },
    preQuestionHandler: function () {
      const currentQuestionIndex = this.questions.indexOf(this.currentQuestion);
      if (currentQuestionIndex > 0) {
        this.currentQuestion = this.questions[currentQuestionIndex - 1];
      }
    },
    userAnswerHandler: function () {
      if (this.currentQuestion.correct && this.currentQuestion.showResult) {
        this.nextQuestionHandler();
        return;
      }
      if (this.currentQuestion.answer === this.currentQuestion.userAnswer) {
        this.currentQuestion.correct = true;
      } else {
        this.currentQuestion.correct = false;
      }

      this.currentQuestion.showResult = true;
    },
  },
};
</script>

<style scoped>
</style>