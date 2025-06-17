<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>波動タイプ診断</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Raleway:wght@300;500;700&display=swap');
    :root {
      --deep-marine: #0d1b2a;
      --star-gold: #d4af37;
      --moonlight: rgba(255,255,255,0.1);
      --card-bg: rgba(255,255,255,0.2);
      --radius: 16px;
      --transition: 0.5s;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background: radial-gradient(circle at top center, #1b263b 0%, #0d1b2a 100%);
      color: white;
      font-family: 'Raleway', sans-serif;
      min-height: 100vh;
      overflow-x: hidden;
    }
    body::before {
      content: '';
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      background: url('https://www.transparenttextures.com/patterns/stardust.png');
      opacity: 0.3;
      z-index: -1;
    }
    header {
      text-align: center;
      padding: 80px 20px 40px;
    }
    header h1 {
      font-family: 'Playfair Display', serif;
      font-size: 3rem;
      letter-spacing: 2px;
      color: var(--star-gold);
      text-shadow: 0 0 10px rgba(212,175,55,0.7);
    }
    header p {
      font-size: 1.2rem;
      margin-top: 12px;
      opacity: 0.8;
    }
    .container {
      max-width: 500px;
      margin: auto;
      padding: 20px;
    }
    .intro, .question-section, .result {
      backdrop-filter: blur(10px);
      background: var(--card-bg);
      border: 1px solid var(--moonlight);
      border-radius: var(--radius);
      margin-bottom: 40px;
      padding: 30px 20px;
      animation: fadeIn 0.8s ease;
    }
    .btn-start, .btn-submit {
      display: block;
      background: linear-gradient(45deg, rgba(212,175,55,0.9), rgba(212,175,55,0.6));
      color: var(--deep-marine);
      font-weight: bold;
      padding: 14px 28px;
      border: none;
      border-radius: var(--radius);
      font-size: 1rem;
      margin: 20px auto 0;
      cursor: pointer;
      transition: transform var(--transition), background var(--transition);
      box-shadow: 0 4px 20px rgba(0,0,0,0.2);
      text-shadow: 0 1px 2px rgba(255,255,255,0.5);
    }
    .btn-start:hover, .btn-submit:hover { transform: scale(1.05); }
    .question-section { display: none; }
    .question { margin-bottom: 30px; }
    .question p {
      font-size: 1.1rem;
      font-weight: 500;
      margin-bottom: 16px;
    }
    .question label {
      display: block;
      background: rgba(255,255,255,0.1);
      border: 2px solid var(--moonlight);
      border-radius: var(--radius);
      padding: 14px 18px;
      margin-bottom: 12px;
      cursor: pointer;
      transition: background var(--transition), border-color var(--transition);
    }
    .question input[type="radio"] { display: none; }
    .question input[type="radio"]:checked + label {
      background: rgba(212,175,55,0.2);
      border-color: var(--star-gold);
    }
    .result { display: none; text-align: center; }
    .result h2 {
      font-family: 'Playfair Display', serif;
      font-size: 2.2rem;
      color: var(--star-gold);
      margin-bottom: 12px;
    }
    .result h3 { font-size: 1.5rem; margin-bottom: 8px; }
    .result p { font-size: 1rem; line-height: 1.6; }
    .sns-share { margin-top: 24px; }
    .sns-share a {
      display: inline-block;
      margin: 0 12px;
      color: var(--star-gold);
      font-weight: bold;
      transition: color var(--transition);
      text-decoration: none;
    }
    .sns-share a:hover { color: white; }
    @keyframes fadeIn { from {opacity:0; transform: translateY(20px);} to {opacity:1; transform:translateY(0);} }
    @media(max-width:600px) {
      header h1 { font-size: 2rem; }
      .container { padding: 10px; }
    }
  </style>
</head>
<body>
  <header>
    <h1>波動タイプ診断</h1>
    <p>12タイプで読み解く、あなたの本質エネルギー</p>
  </header>
  <div class="container">
    <div class="intro" id="introSection">
      <p>8つの質問で、あなたの波動コードを算出します。</p>
      <button class="btn-start" onclick="startQuiz()">診断を始める</button>
    </div>
    <div class="question-section" id="questionSection">
      <form id="diagnosisForm">
        <div class="question">
          <p>Q1. 週末の自由時間、あなたはどちらを選びますか？</p>
          <input type="radio" id="q1a" name="q1" value="1"><label for="q1a">A. 静かな場所でひとり読書や映画鑑賞を楽しむ</label>
          <input type="radio" id="q1b" name="q1" value="6"><label for="q1b">B. 映画館やカフェなど、友達や恋人と出かける</label>
        </div>
        <div class="question">
          <p>Q2. 趣味のグループやSNSオフ会の誘いが来たら？</p>
          <input type="radio" id="q2a" name="q2" value="1"><label for="q2a">A. 気になるけど心の準備が必要</label>
          <input type="radio" id="q2b" name="q2" value="6"><label for="q2b">B. ぜひ参加してみたい！</label>
        </div>
        <div class="question">
          <p>Q3. 初めての場所で過ごすとき、どちらの感覚が近い？</p>
          <input type="radio" id="q3a" name="q3" value="1"><label for="q3a">A. 様子を見ながら静かに過ごす</label>
          <input type="radio" id="q3b" name="q3" value="6"><label for="q3b">B. 新しい出会いや会話にワクワクして話しかける</label>
        </div>
        <div class="question">
          <p>Q4. 新しい習い事や学びを始めるとき、まずあなたが行うのは？</p>
          <input type="radio" id="q4a" name="q4" value="2"><label for="q4a">A. 計画を立てる</label>
          <input type="radio" id="q4b" name="q4" value="4"><label for="q4b">B. 実体験の感想を聞く</label>
          <input type="radio" id="q4c" name="q4" value="8"><label for="q4c">C. 未来の自分をイメージ</label>
        </div>
        <div class="question">
          <p>Q5. 日常のトラブルや悩み相談を受けたとき、あなたは？</p>
          <input type="radio" id="q5a" name="q5" value="2"><label for="q5a">A. 解決手順を順序立てて説明</label>
          <input type="radio" id="q5b" name="q5" value="4"><label for="q5b">B. 気持ちに寄り添って聞く</label>
          <input type="radio" id="q5c" name="q5" value="8"><label for="q5c">C. 未来への影響を語る</label>
        </div>
        <div class="question">
          <p>Q6. 買い物や予算を決めるとき、あなたは何を基準にしますか？</p>
          <input type="radio" id="q6a" name="q6" value="3"><label for="q6a">A. 値段やスペック重視</label>
          <input type="radio" id="q6b" name="q6" value="9"><label for="q6b">B. 心地よさやワクワク感</label>
        </div>
        <div class="question">
          <p>Q7. 大切な人にアドバイスをするとき、あなたは？</p>
          <input type="radio" id="q7a" name="q7" value="3"><label for="q7a">A. 具体的な方法を伝える</label>
          <input type="radio" id="q7b" name="q7" value="9"><label for="q7b">B. 安心できる言葉を先に伝える</label>
        </div>
        <div class="question">
          <p>Q8. 雑誌で「開運○○特集」を見たときの反応は？</p>
          <input type="radio" id="q8a" name="q8" value="3"><label for="q8a">A. 直感的に気になる</label>
          <input type="radio" id="q8b" name="q8" value="9"><label for="q8b">B. 実用性で判断</label>
        </div>
        <button type="submit" class="btn-submit">結果を見る</button>
      </form>
    </div>
    <div class="result" id="resultSection">
      <h2 id="typeCode"></h2>
      <h3 id="typeName"></h3>
      <p id="typeDesc"></p>
      <div class="sns-share">
        <a id="twitterShare" href="#" target="_blank">Xでシェア</a>
        <a id="lineShare" href="#" target="_blank">LINEで送る</a>
      </div>
    </div>
  </div>
<script>
  function startQuiz() {
    document.getElementById('introSection').style.display='none';
    document.getElementById('questionSection').style.display='block';
    document.getElementById('questionSection').scrollIntoView({behavior:'smooth'});
  }
  document.getElementById('diagnosisForm').addEventListener('submit',function(e){
    e.preventDefault();
    const f=new FormData(e.target);
    const c1=[+f.get('q1'),+f.get('q2'),+f.get('q3')],
          c2=[+f.get('q4'),+f.get('q5')],
          c3=[+f.get('q6'),+f.get('q7'),+f.get('q8')];
    const d1=c1.filter(v=>v===1).length>=2?1:6;
    let d2=(c2.filter(v=>v===+f.get('q4')).length===2)?+f.get('q4'):+f.get('q4');
    const d3=c3.filter(v=>v===3).length>=2?3:9;
    const code=`${d1}${d2}${d3}`;
    const typeDetails = {
      '123': { jp:'守護者', en:'Guardian', desc:'「静かに見守る力」「安心の礎」<br>あなたは、目立たないところで周囲を支える存在。誰かのためにそっと手を差し伸べる優しさを持ちながら、自分の気持ちは後回しにしがち。人の期待に応えようと頑張りすぎて、いつの間にか疲れていることも。「私がいなきゃ」の気持ちを、少し手放すことが癒しの第一歩。'},
      '129': { jp:'安定者', en:'Stabilizer', desc:'「平穏を築く」「変わらぬ安心感」<br>あなたは、波立たせない“安らぎの土台”をつくる人。感情に振り回されにくく、物事を長い目で見つめる視点を持つ。一方で、変化が苦手で、自分を閉じ込めてしまうこともある。安定は強さ。けれど時には“未知の選択”にも心を開いてみて。'},
      '143': { jp:'調整者', en:'Mediator', desc:'「視点をつなぐ」「心のバランサー」<br>あなたは、人と人のあいだに立ち、橋をかける人。対立や緊張を和らげ、絶妙な言葉選びで空気を整えるセンスがある。周囲に合わせすぎて、自分の本音が分からなくなると迷いが生じる。調整するあなたこそ、自分の“真ん中の声”に耳を傾けて。'},
      '149': { jp:'癒し手', en:'Healer', desc:'「共感の波動」「心に寄り添う」<br>あなたは、人の痛みを自分のことのように感じられる感受性の持ち主。言葉にならない想いを受け取る力があり、誰かにとっての“癒しの存在”になっていることが多い。ただ、優しさが強すぎて、自分を後回しにしがち。まず、自分を癒すこと。それがあなたの力をさらに広げる鍵になる。'},
      '183': { jp:'戦略家', en:'Strategist', desc:'「未来を描く力」「直感的プランナー」<br>あなたは、“今”の先にある流れを読むのが得意。物事の構造や背景を瞬時に把握し、未来を見据えて行動できる力がある。周囲がまだ気づいていない問題点を察知するがゆえに、孤独を感じることも。その視点はギフト。形にすることで、多くの人を導ける。'},
      '189': { jp:'夢語り', en:'Dreamweaver', desc:'「可能性の紡ぎ手」「理想を現実に近づける」<br>あなたは、夢や希望に命を吹き込む力を持つ人。思い描いた未来に向けて、誰よりも純粋に動き続ける情熱家。ただ、理想と現実のギャップに心が折れそうになることもある。夢は、誰かの道しるべになる。まずは“自分を信じる”ことから始めよう。'},
      '623': { jp:'行動者', en:'Activator', desc:'「瞬発力」「動き始めるエネルギー」<br>あなたは、“感じたらすぐ動く”感覚派。直感に従って動き始めると、大きな流れが一気に動き出すタイプ。逆に、考えすぎるとエネルギーが止まりやすい傾向も。「動けば変わる」があなたのキーワード。小さな一歩から世界は動く。'},
      '629': { jp:'交差者', en:'Connector', desc:'「人をつなぐ」「対話の架け橋」<br>あなたは、人と人との“交差点”になる人。さまざまな人の価値観を受け入れ、自然と人を引き合わせることができる。人間関係に神経を使いすぎて、自分を見失いがちなのが課題。“誰とつながるか”だけでなく、“誰でいたいか”を大切にして。'},
      '643': { jp:'促進者', en:'Facilitator', desc:'「場をつくる」「調和の演出家」<br>あなたは、人が安心して集える“場”を生み出す達人。誰がどこにいると安心するか、どうすればみんなが動き出せるか――そんなことが感覚的にわかる人。ただし、黒子に徹しすぎて目立つことを避けがち。あなたの存在が、空気を変える力になる。もっと自分を前に出していい。'},
      '649': { jp:'調和者', en:'Harmonizer', desc:'「和を尊ぶ」「集団の心をひとつに」<br>あなたは、“場”全体のエネルギーを読むのが得意な人。自分の意見よりも、みんなの気持ちを大切にするがゆえに、対立を避けすぎることもある。「波風立てない」優しさの裏に、自分の“本音”が隠れていないか確認して。'},
      '683': { jp:'開拓者', en:'Pioneer', desc:'「新境地を切り開く」「冒険のエネルギー」<br>あなたは、“誰もやったことがないこと”にワクワクする人。常識に縛られず、新しい可能性を見出すセンスがある反面、孤立したり理解されにくい経験も多い。あなたの“違和感”は突破口。そのまま進めば、道になる。'},
      '689': { jp:'触媒者', en:'Inspirer', desc:'「火種を灯す」「想像を現実に変える」<br>あなたは、人の“可能性の種”に気づく人。何気ない一言が、人の背中を押したり、場を変えたりする。言葉・空気・感情に敏感な分、疲れやすくもある。あなたの存在そのものが、きっかけになる。だからこそ、まず自分を整えて。'}
    };
    const { jp, en, desc } = typeDetails[code] || { jp:'未定義', en:'Undefined', desc:'準備中です' };
    document.getElementById('typeCode').innerText = `波動コード：${code}`;
    document.getElementById('typeName').innerText = `${jp}（${en}）`;
    document.getElementById('typeDesc').innerHTML = desc;
    document.getElementById('questionSection').style.display='none';
    document.getElementById('resultSection').style.display='block';
    const shareUrl = encodeURIComponent(location.href);
    document.getElementById('twitterShare').href = `https://twitter.com/intent/tweet?text=私の波動タイプは「${jp}」でした！&url=${shareUrl}`;
    document.getElementById('lineShare').href = `https://social-plugins.line.me/lineit/share?url=${shareUrl}`;
    document.getElementById('resultSection').scrollIntoView({behavior:'smooth'});
  });
</script>
</body>
</html>

