[中考词汇.html](https://github.com/user-attachments/files/28211959/default.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>中考单词闯关</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }

  :root {
    --bg:       #1e2030;
    --card-bg:  #282a3a;
    --gold:     #f0b428;
    --green:    #5cbf5c;
    --red:     #e05555;
    --blue:    #5090d0;
    --pink:    #d070a0;
    --text:    #e8e4d0;
    --dim:     #9898b0;
    --border:  #484868;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: -apple-system, BlinkMacSystemFont, "PingFang SC", "Microsoft YaHei", "Helvetica Neue", sans-serif;
    min-height: 100vh;
    min-height: 100dvh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 12px;
    background-image:
      radial-gradient(circle at 20% 30%, #2a2c42 0%, transparent 50%),
      radial-gradient(circle at 80% 70%, #242638 0%, transparent 50%);
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
  }

  .container {
    width: 100%;
    max-width: 520px;
    min-height: 90vh;
    min-height: 90dvh;
    display: flex;
    flex-direction: column;
  }

  /* ===== HEADER ===== */
  .top-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 14px 16px;
  }
  .top-bar .logo {
    font-size: 16px;
    font-weight: 700;
    color: var(--gold);
    letter-spacing: 1px;
  }
  .top-bar .badge {
    font-size: 12px;
    color: var(--dim);
    background: #2a2c3e;
    padding: 5px 12px;
    border-radius: 20px;
    border: 1px solid var(--border);
  }

  /* ===== STAGE TABS ===== */
  .tabs {
    display: flex;
    gap: 6px;
    padding: 0 16px 12px;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none;
  }
  .tabs::-webkit-scrollbar { display: none; }
  .tab {
    flex-shrink: 0;
    padding: 8px 14px;
    border-radius: 20px;
    border: 2px solid var(--border);
    background: transparent;
    color: var(--dim);
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s;
    font-family: inherit;
    white-space: nowrap;
  }
  .tab.done { border-color: var(--green); color: var(--green); background: #1a2a1a; }
  .tab.current { border-color: var(--gold); color: var(--gold); background: #2a2410; }
  .tab.locked { opacity: 0.35; }

  /* ===== PROGRESS ===== */
  .progress-row {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 0 16px 8px;
  }
  .progress-bar {
    flex: 1;
    height: 8px;
    background: #2a2c3e;
    border-radius: 4px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--green), #3a9a3a);
    border-radius: 4px;
    transition: width 0.3s;
  }
  .progress-num {
    font-size: 11px;
    color: var(--dim);
    white-space: nowrap;
    min-width: 40px;
    text-align: right;
  }

  /* ===== CARD ===== */
  .card-container {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 8px 16px;
    perspective: 1000px;
  }

  .card {
    width: 100%;
    background: var(--card-bg);
    border: 2px solid var(--border);
    border-radius: 16px;
    padding: 24px 20px;
    text-align: center;
    cursor: pointer;
    transition: border-color 0.2s, transform 0.15s;
    position: relative;
    min-height: 240px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;
  }
  .card:active { transform: scale(0.98); }
  .card.flipped { border-color: var(--blue); }

  .card .tag {
    font-size: 10px;
    color: var(--pink);
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  .card .word {
    font-size: 32px;
    font-weight: 800;
    color: #fff;
    letter-spacing: 1px;
    line-height: 1.2;
  }
  .card .ipa {
    font-size: 14px;
    color: var(--dim);
  }
  .card .type {
    font-size: 12px;
    color: var(--blue);
  }
  .card .tap-hint {
    font-size: 12px;
    color: #666;
    margin-top: 4px;
  }

  .card .detail { display: none; }
  .card.flipped .detail { display: flex; flex-direction: column; gap: 10px; }
  .card.flipped .tap-hint { display: none; }

  .card .zh {
    font-size: 24px;
    font-weight: 700;
    color: var(--gold);
  }
  .card .example {
    font-size: 14px;
    color: #bbb;
    line-height: 1.7;
    font-style: italic;
  }
  .card .note {
    font-size: 13px;
    color: var(--pink);
    line-height: 1.6;
    background: #2a2028;
    padding: 10px 14px;
    border-radius: 10px;
    border-left: 3px solid var(--pink);
  }

  /* ===== SWIPE HINT ===== */
  .swipe-hint {
    display: flex;
    gap: 20px;
    justify-content: center;
    padding: 4px;
    font-size: 11px;
    color: #555;
  }

  /* ===== BUTTONS ===== */
  .btn-row {
    display: flex;
    gap: 12px;
    padding: 12px 16px 20px;
    justify-content: center;
  }
  .btn {
    flex: 1; max-width: 180px;
    padding: 14px 0;
    border-radius: 14px;
    border: none;
    font-size: 15px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.15s;
    font-family: inherit;
    letter-spacing: 0.5px;
  }
  .btn:active { transform: scale(0.95); }
  .btn-yes { background: #1a3a1a; color: var(--green); border: 2px solid var(--green); }
  .btn-yes:active { background: #2a4a2a; }
  .btn-no  { background: #3a1a1a; color: #f08080; border: 2px solid #803030; }
  .btn-no:active { background: #4a1a1a; }

  .btn-full {
    width: 100%; max-width: 300px;
    padding: 16px;
    background: var(--gold);
    color: #1a1c2c;
    font-size: 16px;
    font-weight: 700;
    border: none;
    border-radius: 14px;
    cursor: pointer;
    font-family: inherit;
    letter-spacing: 1px;
    transition: all 0.15s;
  }
  .btn-full:active { transform: scale(0.95); background: #e5a820; }

  /* ===== TITLE SCREEN ===== */
  .title-box {
    text-align: center;
    padding: 20px 0;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 16px;
  }
  .title-box .icon { font-size: 56px; }
  .title-box h2 { font-size: 20px; color: var(--gold); }
  .title-box p { font-size: 13px; color: var(--dim); line-height: 1.8; max-width: 320px; }
  .stats {
    display: flex;
    gap: 20px;
    justify-content: center;
  }
  .stat {
    background: #2a2c3e;
    border-radius: 12px;
    padding: 14px 18px;
    text-align: center;
    border: 1px solid var(--border);
  }
  .stat .val { font-size: 24px; font-weight: 700; color: var(--gold); }
  .stat .lbl { font-size: 11px; color: var(--dim); margin-top: 2px; }

  /* ===== COMPLETE ===== */
  .done-box {
    text-align: center;
    padding: 30px 0;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 12px;
  }
  .done-box .trophy { font-size: 56px; }
  .done-box h3 { font-size: 18px; color: var(--gold); }
  .done-box .sub { font-size: 13px; color: var(--green); }

  /* toast */
  .toast {
    position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
    background: var(--green); color: #fff;
    padding: 10px 24px; border-radius: 20px;
    font-size: 14px; font-weight: 600;
    z-index: 999; opacity: 0; transition: opacity 0.3s;
    pointer-events: none;
  }
  .toast.show { opacity: 1; }
</style>
</head>
<body>

<div class="container" id="app"></div>
<div class="toast" id="toast"></div>

<script>
const STAGES = [
  {
    name: "基础高频", icon: "⭐",
    words: [
      { en: "absent", ipa: "/ˈæbsənt/", type: "adj.", zh: "缺席的", ex: "He was <b>absent</b> from school yesterday.", note: "搭配：be absent from（缺席某场合）" },
      { en: "achieve", ipa: "/əˈtʃiːv/", type: "v.", zh: "实现，达到", ex: "She <b>achieved</b> her goal.", note: "achieve success/dream；名词 achievement" },
      { en: "against", ipa: "/əˈɡenst/", type: "prep.", zh: "反对；紧靠", ex: "They are <b>against</b> the plan.", note: "play against(对抗)；against the wall(靠墙)" },
      { en: "attend", ipa: "/əˈtend/", type: "v.", zh: "参加，出席", ex: "All must <b>attend</b> the meeting.", note: "attend school/class；名词 attendance" },
      { en: "available", ipa: "/əˈveɪləbl/", type: "adj.", zh: "可获得的；有空的", ex: "Is this seat <b>available</b>?", note: "sth is available to sb（某人可获得某物）" },
      { en: "avoid", ipa: "/əˈvɔɪd/", type: "v.", zh: "避免", ex: "<b>Avoid</b> making the same mistake.", note: "avoid doing（+doing，不是+to do）" },
      { en: "belong", ipa: "/bɪˈlɒŋ/", type: "v.", zh: "属于", ex: "This book <b>belongs</b> to me.", note: "belong to（无被动、无进行时）" },
      { en: "breathe", ipa: "/briːð/", type: "v.", zh: "呼吸", ex: "<b>Breathe</b> deeply.", note: "动词 breathe(有e) ≠ 名词 breath(无e)" },
      { en: "celebrate", ipa: "/ˈselɪbreɪt/", type: "v.", zh: "庆祝", ex: "We <b>celebrated</b> New Year.", note: "名词 celebration；celebrate + 节日" },
      { en: "compare", ipa: "/kəmˈpeə(r)/", type: "v.", zh: "比较；比喻", ex: "<b>Compared</b> with last year, it grew.", note: "compare A with B(对比)；compare A to B(比作)" },
      { en: "complete", ipa: "/kəmˈpliːt/", type: "v./adj.", zh: "完成；完全的", ex: "Have you <b>completed</b> the form?", note: "complete(全部完成) vs finish(结束)" },
      { en: "connect", ipa: "/kəˈnekt/", type: "v.", zh: "连接", ex: "The bridge <b>connects</b> two cities.", note: "connect A with/to B；名词 connection" },
      { en: "consider", ipa: "/kənˈsɪdə(r)/", type: "v.", zh: "考虑", ex: "I'm <b>considering</b> changing jobs.", note: "consider doing（+doing，不是+to do）" },
      { en: "continue", ipa: "/kənˈtɪnjuː/", type: "v.", zh: "继续", ex: "She <b>continued</b> reading.", note: "continue doing / to do 均可" },
      { en: "create", ipa: "/kriˈeɪt/", type: "v.", zh: "创造", ex: "Artists <b>create</b> beauty.", note: "名词 creation；adj. creative" },
      { en: "decide", ipa: "/dɪˈsaɪd/", type: "v.", zh: "决定", ex: "They <b>decided</b> to go.", note: "decide to do；名词 decision" },
      { en: "depend", ipa: "/dɪˈpend/", type: "v.", zh: "依赖", ex: "It <b>depends</b> on you.", note: "depend on = rely on；It depends.(看情况)" },
      { en: "describe", ipa: "/dɪˈskraɪb/", type: "v.", zh: "描述", ex: "<b>Describe</b> what happened.", note: "名词 description；describe sth to sb" },
      { en: "develop", ipa: "/dɪˈveləp/", type: "v.", zh: "发展；培养", ex: "Reading <b>develops</b> your mind.", note: "developing(发展中) vs developed(发达)" },
      { en: "discover", ipa: "/dɪˈskʌvə(r)/", type: "v.", zh: "发现", ex: "They <b>discovered</b> a new planet.", note: "discover(发现已有) vs invent(发明新的)" },
    ]
  },
  {
    name: "易混淆词", icon: "🔍",
    words: [
      { en: "accept / receive", ipa: "", type: "v.", zh: "接受 / 收到", ex: "I <b>received</b> it but didn't <b>accept</b> it.", note: "receive=客观上收到；accept=主观上接受。收到≠接受！" },
      { en: "affect / effect", ipa: "", type: "v. / n.", zh: "影响(v.) / 效果(n.)", ex: "Weather <b>affects</b> mood. The <b>effect</b> is clear.", note: "affect=动词；effect=名词(效果)/动词(实现)" },
      { en: "borrow / lend", ipa: "", type: "v.", zh: "借入 / 借出", ex: "Can I <b>borrow</b> your pen? I'll <b>lend</b> it to you.", note: "borrow+from(借入←)；lend+to(借出→)" },
      { en: "bring / take", ipa: "", type: "v.", zh: "拿来 / 带去", ex: "<b>Bring</b> it here. <b>Take</b> it home.", note: "bring=朝说话人方向来；take=朝别处去" },
      { en: "few / a few / little / a little", ipa: "", type: "adj.", zh: "很少 / 有几个 / 很少 / 有一点", ex: "I have <b>a few</b> friends. I have <b>few</b> enemies.", note: "few+可数；little+不可数。有a=肯定，无a=否定" },
      { en: "hear / listen", ipa: "", type: "v.", zh: "听见 / 听（注意听）", ex: "I <b>heard</b> a noise. <b>Listen</b> to me!", note: "hear=无意中听到(结果)；listen to=有意识听(过程)" },
      { en: "look / see / watch", ipa: "", type: "v.", zh: "看 / 看见 / 观看", ex: "<b>Look</b> at this. I <b>see</b> it. I <b>watched</b> TV.", note: "look=有意识看(+at)；see=看见(结果)；watch=专注观看" },
      { en: "remember / remind", ipa: "", type: "v.", zh: "记住 / 提醒", ex: "I <b>remember</b> him. <b>Remind</b> me to call.", note: "remember to do(记得去做) vs doing(记得做过)" },
      { en: "say / tell / speak / talk", ipa: "", type: "v.", zh: "说 / 告诉 / 讲 / 交谈", ex: "He <b>said</b> hi. She <b>told</b> me. He <b>speaks</b> EN.", note: "say+内容；tell+人；speak+语言；talk+with" },
      { en: "spend / cost / take / pay", ipa: "", type: "v.", zh: "花费（四种说法）", ex: "I <b>spent</b> ¥10. It <b>costs</b> ¥10. It <b>took</b> 2h. I <b>paid</b> ¥10.", note: "spend-人主语；cost-物主语；take-it主语(时间)；pay-人+for" },
      { en: "used to / be used to", ipa: "", type: "v./adj.", zh: "过去常常 / 习惯于", ex: "I <b>used to</b> smoke. I <b>am used to</b> getting up early.", note: "used to do(过去常做)；be used to doing(习惯做)" },
      { en: "alone / lonely", ipa: "", type: "adj.", zh: "独自一人 / 孤独的", ex: "He lives <b>alone</b> but isn't <b>lonely</b>.", note: "alone=客观独自；lonely=内心孤独(负面)" },
      { en: "rise / raise", ipa: "", type: "v.", zh: "上升(vi.) / 举起(vt.)", ex: "The sun <b>rises</b>. She <b>raised</b> her hand.", note: "rise-rose-risen(不及物)；raise-raised(及物+宾语)" },
      { en: "lie / lay", ipa: "", type: "v.", zh: "躺；说谎 / 放置；下蛋", ex: "He <b>lay</b> down. The hen <b>laid</b> an egg.", note: "lie(躺)-lay-lain；lie(说谎)-lied；lay(放/下蛋)-laid" },
      { en: "except / besides", ipa: "", type: "prep.", zh: "除…外(排除) / 除…外(包括)", ex: "All went <b>except</b> Tom. <b>Besides</b> Tom, Jack went.", note: "except=排除；besides=附加" },
      { en: "across / through", ipa: "", type: "prep.", zh: "穿过(表面) / 穿过(内部)", ex: "Walk <b>across</b> the road. Go <b>through</b> the tunnel.", note: "across=表面横穿；through=内部纵穿" },
      { en: "arrive / reach / get", ipa: "", type: "v.", zh: "到达", ex: "<b>Arrive</b> at school. <b>Reach</b> Shanghai. <b>Get</b> to school.", note: "arrive at/in；reach+地点(及物)；get to+地点" },
      { en: "other / another / the other", ipa: "", type: "adj.", zh: "其他的/另一个/(两个中)另一个", ex: "<b>Another</b> question. One red, <b>the other</b> blue.", note: "other+复数；another+单数；the other=两个中另一个" },
      { en: "so...that / such...that", ipa: "", type: "conj.", zh: "如此…以至于", ex: "She is <b>so</b> kind <b>that</b> all love her.", note: "so+adj./adv.+that；such+名词短语+that" },
      { en: "invent / discover", ipa: "", type: "v.", zh: "发明 / 发现", ex: "Edison <b>invented</b> the bulb. Columbus <b>discovered</b> America.", note: "invent=创造新东西；discover=发现已存在的东西" },
    ]
  },
  {
    name: "短语搭配", icon: "🔗",
    words: [
      { en: "give up", ipa: "", type: "phr.", zh: "放弃", ex: "Never <b>give up</b> on your dreams.", note: "give up doing = stop trying" },
      { en: "look forward to", ipa: "", type: "phr.", zh: "期待", ex: "I'm <b>looking forward to</b> seeing you.", note: "to是介词！后接 doing/sth。信件常用结尾" },
      { en: "take part in", ipa: "", type: "phr.", zh: "参加", ex: "Many <b>took part in</b> the sports meeting.", note: "= join in = participate in" },
      { en: "pay attention to", ipa: "", type: "phr.", zh: "注意", ex: "<b>Pay attention to</b> the lights.", note: "to是介词 + doing/sth" },
      { en: "make up one's mind", ipa: "", type: "phr.", zh: "下定决心", ex: "She <b>made up her mind</b> to study hard.", note: "= decide firmly；make up one's mind to do" },
      { en: "take care of", ipa: "", type: "phr.", zh: "照顾", ex: "<b>Take care of</b> my dog please.", note: "= look after = care for" },
      { en: "come up with", ipa: "", type: "phr.", zh: "想出（主意）", ex: "He <b>came up with</b> a great idea.", note: "= think of / put forward（提出想法、方案）" },
      { en: "run out of", ipa: "", type: "phr.", zh: "用完", ex: "We've <b>run out of</b> water.", note: "sth runs out(物主语)；sb runs out of sth(人主语)" },
      { en: "get along with", ipa: "", type: "phr.", zh: "与…相处", ex: "I <b>get along</b> well <b>with</b> classmates.", note: "= get on with" },
      { en: "put off", ipa: "", type: "phr.", zh: "推迟", ex: "Don't <b>put off</b> today's work.", note: "= delay；put off doing" },
      { en: "turn down", ipa: "", type: "phr.", zh: "拒绝；调低音量", ex: "She <b>turned down</b> the offer.", note: "= refuse/reject；turn down the volume(调低)" },
      { en: "set off", ipa: "", type: "phr.", zh: "出发", ex: "We <b>set off</b> early.", note: "= set out = start a journey" },
      { en: "break down", ipa: "", type: "phr.", zh: "出故障", ex: "The car <b>broke down</b>.", note: "机器/车辆抛锚专用" },
      { en: "hold on", ipa: "", type: "phr.", zh: "等一下；坚持", ex: "<b>Hold on</b> a minute!", note: "电话用语=等一下；hold on to=抓住不放" },
      { en: "make use of", ipa: "", type: "phr.", zh: "利用", ex: "<b>Make good use of</b> your time.", note: "= take advantage of" },
      { en: "keep on", ipa: "", type: "phr.", zh: "继续做", ex: "She <b>kept on</b> asking.", note: "keep on doing = continue doing" },
      { en: "not only...but also...", ipa: "", type: "conj.", zh: "不仅…而且…", ex: "He <b>not only</b> sings <b>but also</b> dances.", note: "句首要倒装：Not only does he sing..." },
      { en: "neither...nor...", ipa: "", type: "conj.", zh: "既不…也不…", ex: "She likes <b>neither</b> coffee <b>nor</b> tea.", note: "= 两者都不；就近原则" },
      { en: "either...or...", ipa: "", type: "conj.", zh: "要么…要么…", ex: "You can <b>either</b> stay <b>or</b> leave.", note: "= 二者选一；就近原则" },
      { en: "carry out", ipa: "", type: "phr.", zh: "执行，实施", ex: "The plan was <b>carried out</b> well.", note: "= conduct/implement；carry out a survey" },
    ]
  },
  {
    name: "词形转换", icon: "🔄",
    words: [
      { en: "succeed / success / successful", ipa: "", type: "v./n./adj.", zh: "成功", ex: "She <b>succeeded</b>. It's a <b>success</b>. She's <b>successful</b>.", note: "succeed in doing；achieve success；be successful in" },
      { en: "choose / choice", ipa: "", type: "v./n.", zh: "选择", ex: "You <b>choose</b>. It's your <b>choice</b>.", note: "choose-chose-chosen；have no choice but to do" },
      { en: "explain / explanation", ipa: "", type: "v./n.", zh: "解释", ex: "<b>Explain</b> it. No <b>explanation</b>.", note: "explain sth to sb（× explain sb sth）" },
      { en: "die / dead / death", ipa: "", type: "v./adj./n.", zh: "死/死的/死亡", ex: "He <b>died</b>. He is <b>dead</b>. His <b>death</b> shocked us.", note: "die(瞬间动词)；be dead(状态)；die of(内因)/from(外因)" },
      { en: "please / pleased / pleasant / pleasure", ipa: "", type: "v./adj./adj./n.", zh: "高兴(四种形式)", ex: "I'm <b>pleased</b>. It's <b>pleasant</b>. With <b>pleasure</b>.", note: "pleased(人高兴)；pleasant(物令人愉快)；with pleasure(乐意)" },
      { en: "interest / interested / interesting", ipa: "", type: "n./adj./adj.", zh: "兴趣", ex: "I'm <b>interested</b>. It's <b>interesting</b>.", note: "人+ed(感到…)；物+ing(令人…)。同类：excited/exciting等" },
      { en: "possible / possibly / impossible", ipa: "", type: "adj./adv./adj.", zh: "可能的/可能地/不可能的", ex: "It's <b>possible</b>. If <b>possibly</b>. It's <b>impossible</b>.", note: "as...as possible；名词 possibility" },
      { en: "safe / safely / safety", ipa: "", type: "adj./adv./n.", zh: "安全的/安全地/安全", ex: "Stay <b>safe</b>. Drive <b>safely</b>. <b>Safety</b> first.", note: "形/副/名三步变形，逐个记！" },
      { en: "important / importance", ipa: "", type: "adj./n.", zh: "重要的/重要性", ex: "It's <b>important</b>. It's of <b>importance</b>.", note: "be of importance = be important" },
      { en: "different / difference", ipa: "", type: "adj./n.", zh: "不同的/差异", ex: "They are <b>different</b>. There's a <b>difference</b>.", note: "be different from；make a difference(有影响)" },
      { en: "true / truth / truly", ipa: "", type: "adj./n./adv.", zh: "真的/真相/真正地", ex: "Is it <b>true</b>? Tell the <b>truth</b>. I'm <b>truly</b> sorry.", note: "true→truth(去e加th)；true→truly(去e加ly)" },
      { en: "wide / width / widen", ipa: "", type: "adj./n./v.", zh: "宽的/宽度/变宽", ex: "10m <b>wide</b>. Its <b>width</b>. They <b>widened</b> it.", note: "wide→width→widen。同理：long→length→lengthen" },
      { en: "advise / advice", ipa: "", type: "v./n.", zh: "建议(动词/名词)", ex: "I <b>advise</b> you to wait. Some <b>advice</b>.", note: "动词 advise(se发z)；名词 advice(ce发s,不可数)" },
      { en: "worry / worried / worrying", ipa: "", type: "v./adj./adj.", zh: "担心/担忧的/令人担忧的", ex: "Don't <b>worry</b>. She's <b>worried</b>. It's <b>worrying</b>.", note: "be worried about；人用worried，事用worrying" },
      { en: "know / knowledge", ipa: "", type: "v./n.", zh: "知道/知识", ex: "Do you <b>know</b>? <b>Knowledge</b> is power.", note: "knowledge 不可数！have a good knowledge of" },
      { en: "serve / service", ipa: "", type: "v./n.", zh: "服务", ex: "He <b>served</b> us. Good <b>service</b>.", note: "serve sb(直接+人,不加for)" },
      { en: "introduce / introduction", ipa: "", type: "v./n.", zh: "介绍", ex: "<b>Introduce</b> yourself. No <b>introduction</b>.", note: "introduce A to B" },
      { en: "weigh / weight", ipa: "", type: "v./n.", zh: "称重/重量", ex: "It <b>weighs</b> 5kg. Its <b>weight</b> is 5kg.", note: "weigh+数字(动词)；lose weight(减肥)" },
      { en: "breathe / breath", ipa: "", type: "v./n.", zh: "呼吸(动/名)", ex: "<b>Breathe</b> in. Take a deep <b>breath</b>.", note: "动词有e发ð；名词无e发θ。必考！" },
      { en: "manage / manager / management", ipa: "", type: "v./n./n.", zh: "管理/经理/管理(抽象)", ex: "He <b>manages</b> the team. He's the <b>manager</b>.", note: "manage to do = 设法成功做到" },
    ]
  },
  {
    name: "冲刺易错", icon: "🏆",
    words: [
      { en: "prevent", ipa: "/prɪˈvent/", type: "v.", zh: "阻止", ex: "Rain <b>prevented</b> us from going.", note: "prevent sb (from) doing = stop/keep sb from doing" },
      { en: "provide", ipa: "/prəˈvaɪd/", type: "v.", zh: "提供", ex: "The school <b>provides</b> students with books.", note: "provide sb with sth = provide sth for sb" },
      { en: "require", ipa: "/rɪˈkwaɪə(r)/", type: "v.", zh: "需要；要求", ex: "The job <b>requires</b> patience.", note: "require doing = require to be done = need doing" },
      { en: "separate", ipa: "/ˈsepəreɪt/", type: "v.", zh: "分开", ex: "<b>Separate</b> good apples from bad.", note: "separate A from B；separate分开(原有联系) vs divide分割" },
      { en: "suppose", ipa: "/səˈpəʊz/", type: "v.", zh: "认为；应该", ex: "You <b>are supposed to</b> arrive on time.", note: "be supposed to do = should do。高频考点！" },
      { en: "wonder", ipa: "/ˈwʌndə(r)/", type: "v.", zh: "想知道", ex: "I <b>wonder</b> if he'll come.", note: "wonder if/whether；no wonder(难怪)" },
      { en: "afford", ipa: "/əˈfɔːd/", type: "v.", zh: "负担得起", ex: "I can't <b>afford</b> a new car.", note: "can/could afford sth / to do" },
      { en: "allow", ipa: "/əˈlaʊ/", type: "v.", zh: "允许", ex: "Smoking is not <b>allowed</b>.", note: "allow sb to do；allow doing；be allowed to do" },
      { en: "encourage", ipa: "/ɪnˈkʌrɪdʒ/", type: "v.", zh: "鼓励", ex: "She <b>encouraged</b> me to try again.", note: "encourage sb to do；反义词 discourage" },
      { en: "expect", ipa: "/ɪkˈspekt/", type: "v.", zh: "期望；预计", ex: "I <b>expect</b> to see him soon.", note: "expect to do / expect sb to do / expect that" },
      { en: "explain", ipa: "/ɪkˈspleɪn/", type: "v.", zh: "解释", ex: "<b>Explain</b> this rule to me.", note: "explain sth to sb（× explain sb sth）" },
      { en: "imagine", ipa: "/ɪˈmædʒɪn/", type: "v.", zh: "想象", ex: "Can you <b>imagine</b> living on Mars?", note: "imagine doing；imagination(想象力)" },
      { en: "include", ipa: "/ɪnˈkluːd/", type: "v.", zh: "包括", ex: "The price <b>includes</b> tax.", note: "including sb = sb included" },
      { en: "offer", ipa: "/ˈɒfə(r)/", type: "v.", zh: "主动提供", ex: "He <b>offered</b> me a cup of tea.", note: "offer sb sth = offer sth to sb；offer to do" },
      { en: "prefer", ipa: "/prɪˈfɜː(r)/", type: "v.", zh: "更喜欢", ex: "I <b>prefer</b> tea to coffee.", note: "prefer A to B；prefer doing to doing；prefer to do rather than do" },
      { en: "regret", ipa: "/rɪˈɡret/", type: "v.", zh: "后悔", ex: "I <b>regret</b> telling him.", note: "regret doing(后悔做了)；regret to do(遗憾地说)" },
      { en: "suggest", ipa: "/səˈdʒest/", type: "v.", zh: "建议", ex: "I <b>suggest</b> going by bus.", note: "suggest doing；suggest that sb (should) do。× suggest sb to do！" },
      { en: "appear", ipa: "/əˈpɪə(r)/", type: "v.", zh: "出现；似乎", ex: "He <b>appeared</b> suddenly. He <b>appears</b> happy.", note: "appear = seem(系动词)；appear to do / that" },
      { en: "mention", ipa: "/ˈmenʃn/", type: "v.", zh: "提到", ex: "He didn't <b>mention</b> the problem.", note: "mention doing / that；don't mention it(不用谢)" },
      { en: "practise", ipa: "/ˈpræktɪs/", type: "v.", zh: "练习", ex: "<b>Practise</b> speaking every day.", note: "practise doing。名词 practice(美式也拼practise)。英式：动practise名practice" },
    ]
  }
];

// ============ APP ============
const APP = document.getElementById("app");
const TOAST = document.getElementById("toast");
const KEY = "zk_mobile_vocab";

function load() { try { return JSON.parse(localStorage.getItem(KEY)) || {}; } catch(e) { return {}; } }
function save(d) { localStorage.setItem(KEY, JSON.stringify(d)); }

let s = {
  progress: load(),
  stage: 0,
  idx: 0,
  screen: "title",
  flipped: false,
  touchStartX: 0, touchStartY: 0,
};
STAGES.forEach((_, i) => { if (!s.progress[i]) s.progress[i] = { mastered: [], currentIdx: 0 }; });

function toast(msg) {
  TOAST.textContent = msg; TOAST.classList.add("show");
  setTimeout(() => TOAST.classList.remove("show"), 1200);
}

function render() {
  APP.innerHTML = "";

  // Top bar
  const top = document.createElement("div");
  top.className = "top-bar";
  top.innerHTML = `<span class="logo">📖 中考单词闯关</span><span class="badge">上海中考</span>`;
  APP.appendChild(top);

  // Tabs
  const tabs = document.createElement("div");
  tabs.className = "tabs";
  STAGES.forEach((st, i) => {
    const t = document.createElement("button");
    t.className = "tab";
    if (i === s.stage) t.classList.add("current");
    const done = (s.progress[i]?.mastered || []).length >= st.words.length;
    if (done) t.classList.add("done");
    if (i > 0) {
      const prevDone = (s.progress[i-1]?.mastered || []).length >= STAGES[i-1].words.length;
      if (!prevDone) t.classList.add("locked");
    }
    t.textContent = st.icon + " " + st.name;
    t.addEventListener("click", () => {
      if (t.classList.contains("locked")) return;
      s.stage = i; s.screen = "learn"; s.idx = s.progress[i]?.currentIdx || 0; s.flipped = false; render();
    });
    tabs.appendChild(t);
  });
  APP.appendChild(tabs);

  // Progress
  const pd = s.progress[s.stage] || { mastered: [], currentIdx: 0 };
  const done = pd.mastered?.length || 0;
  const total = STAGES[s.stage].words.length;
  const pct = total > 0 ? (done/total*100) : 0;

  const pr = document.createElement("div");
  pr.className = "progress-row";
  pr.innerHTML = `<div class="progress-bar"><div class="progress-fill" style="width:${pct}%"></div></div><div class="progress-num">${done}/${total}</div>`;
  APP.appendChild(pr);

  // Main content
  const main = document.createElement("div");
  main.className = "card-container";

  if (s.screen === "title") {
    let td = 0; STAGES.forEach((st, i) => { td += (s.progress[i]?.mastered || []).length; });
    const tt = STAGES.reduce((a,st) => a + st.words.length, 0);
    main.innerHTML = `
      <div class="title-box">
        <div class="icon">📚</div>
        <h2>上海中考单词闯关</h2>
        <p>100个核心高频+易错词汇<br>点卡片翻面 · 标记掌握 · 五关全通</p>
        <div class="stats">
          <div class="stat"><div class="val">${td}/${tt}</div><div class="lbl">总进度</div></div>
          <div class="stat"><div class="val">5</div><div class="lbl">关卡</div></div>
        </div>
        <button class="btn-full" id="startBtn">▶ 开始闯关</button>
      </div>
    `;
    APP.appendChild(main);
    document.getElementById("startBtn").addEventListener("click", () => {
      s.screen = "learn"; s.stage = 0; s.idx = s.progress[0]?.currentIdx || 0; s.flipped = false; render();
    });
    return;
  }

  if (s.screen === "learn") {
    const stage = STAGES[s.stage];
    const words = stage.words;

    if (s.idx >= words.length) {
      main.innerHTML = `
        <div class="done-box">
          <div class="trophy">🏆</div>
          <h3>${stage.name} 通关！</h3>
          <p class="sub">${done}/${total} 词已掌握</p>
          <button class="btn-full" id="nextBtn">▶ 下一关</button>
          <button class="btn-full" id="retryBtn" style="background:transparent;color:var(--dim);border:2px solid var(--border);margin-top:8px">🔄 复习本关</button>
        </div>
      `;
      APP.appendChild(main);
      document.getElementById("nextBtn")?.addEventListener("click", nextStage);
      document.getElementById("retryBtn")?.addEventListener("click", () => {
        s.idx = 0; s.progress[s.stage].currentIdx = 0; s.flipped = false; render();
      });
      return;
    }

    const word = words[s.idx];
    const isM = (pd.mastered || []).includes(s.idx);

    // Card
    const card = document.createElement("div");
    card.className = "card" + (s.flipped ? " flipped" : "");
    card.id = "wordCard";
    card.innerHTML = `
      <div class="tag">${stage.icon} ${stage.name} · ${s.idx+1}/${total} ${isM ? '✅' : ''}</div>
      <div class="word">${word.en}</div>
      <div class="ipa">${word.ipa}</div>
      <div class="type">${word.type}</div>
      <div class="tap-hint">👆 点击翻卡看释义</div>
      <div class="detail">
        <div class="zh">${word.zh}</div>
        <div class="example">${word.ex}</div>
        <div class="note">💡 ${word.note}</div>
      </div>
    `;

    // Click to flip
    card.addEventListener("click", (e) => {
      if (s.flipped) return;
      s.flipped = true;
      render();
    });

    // Touch swipe
    card.addEventListener("touchstart", (e) => {
      s.touchStartX = e.touches[0].clientX;
      s.touchStartY = e.touches[0].clientY;
    }, { passive: true });
    card.addEventListener("touchend", (e) => {
      const dx = e.changedTouches[0].clientX - s.touchStartX;
      const dy = e.changedTouches[0].clientY - s.touchStartY;
      if (Math.abs(dx) > Math.abs(dy) && Math.abs(dx) > 60) {
        // swipe
        if (s.flipped) {
          if (dx < 0) {
            // swipe left = got it
            markKnown();
          } else {
            // swipe right = review
            markUnknown();
          }
        }
      }
    });

    main.appendChild(card);

    // Swipe hint
    if (s.flipped) {
      const hint = document.createElement("div");
      hint.className = "swipe-hint";
      hint.innerHTML = "<span>👈 左滑 = 再记记</span><span>掌握了 = 右滑 👉</span>";
      main.appendChild(hint);
    }

    // Buttons
    if (s.flipped) {
      const btnRow = document.createElement("div");
      btnRow.className = "btn-row";
      btnRow.innerHTML = `
        <button class="btn btn-yes" id="yesBtn">✅ 掌握了</button>
        <button class="btn btn-no" id="noBtn">❌ 再记记</button>
      `;
      main.appendChild(btnRow);
      document.getElementById("yesBtn").addEventListener("click", markKnown);
      document.getElementById("noBtn").addEventListener("click", markUnknown);
    }

    APP.appendChild(main);
  }

  save(s.progress);
}

function markKnown() {
  const p = s.progress[s.stage];
  if (!p.mastered) p.mastered = [];
  if (!p.mastered.includes(s.idx)) { p.mastered.push(s.idx); toast("✅ 已掌握 +1"); }
  else { toast("已标记过啦"); }
  p.currentIdx = s.idx + 1;
  s.idx = p.currentIdx; s.flipped = false;
  render();
}

function markUnknown() {
  const p = s.progress[s.stage];
  p.currentIdx = s.idx + 1;
  s.idx = p.currentIdx; s.flipped = false;
  toast("🔁 稍后复习");
  render();
}

function nextStage() {
  if (s.stage < STAGES.length - 1) {
    s.stage++;
    s.idx = s.progress[s.stage]?.currentIdx || 0;
    s.flipped = false; render();
  } else {
    let td = 0; STAGES.forEach((st, i) => { td += (s.progress[i]?.mastered || []).length; });
    document.querySelector(".card-container").innerHTML = `
      <div class="done-box">
        <div class="trophy">🎉</div>
        <h3>ALL CLEAR! 全通关!</h3>
        <p class="sub">100词 · 已掌握 ${td} 词</p>
        <p style="color:var(--gold);font-size:13px;margin-top:4px">中考英语，稳了！💪</p>
        <button class="btn-full" id="resetBtn" style="margin-top:12px">🔄 重置</button>
      </div>
    `;
    document.getElementById("resetBtn")?.addEventListener("click", () => {
      if (confirm("确定重置所有进度？")) {
        s.progress = {}; STAGES.forEach((_,i) => { s.progress[i] = { mastered: [], currentIdx: 0 }; });
        s.stage = 0; s.idx = 0; s.screen = "title"; s.flipped = false; render();
      }
    });
  }
}

render();
</script>
</body>
</html>
