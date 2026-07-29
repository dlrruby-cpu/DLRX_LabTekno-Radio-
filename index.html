const PAYPAL_USER_NAME = 'DAVIDLOPEZDALOREX';
const STORAGE_PREFIX = 'labtekno_';

const DEFAULT_STICKERS = [
  'https://via.placeholder.com/120x60/00f3ff/000000?text=DALOREX+LAB',
  'https://via.placeholder.com/90x90/ff0055/ffffff?text=TEKNO+RADIO'
];

function initStickerSystem() {
  const container = document.getElementById('stickersContainer');
  const uploadInput = document.getElementById('stickerUpload');
  if (!container || !uploadInput) return;

  let savedStickers = JSON.parse(localStorage.getItem(STORAGE_PREFIX + 'stickers') || 'null');
  if (!savedStickers || savedStickers.length === 0) {
    savedStickers = DEFAULT_STICKERS;
  }

  renderStickers(savedStickers);

  uploadInput.addEventListener('change', function(e) {
    const files = e.target.files;
    if (!files || files.length === 0) return;
    const newStickers = [...savedStickers];
    let loadedCount = 0;

    Array.from(files).forEach(file => {
      const reader = new FileReader();
      reader.onload = function(event) {
        newStickers.push(event.target.result);
        loadedCount++;
        if (loadedCount === files.length) {
          localStorage.setItem(STORAGE_PREFIX + 'stickers', JSON.stringify(newStickers));
          renderStickers(newStickers);
        }
      };
      reader.readAsDataURL(file);
    });
  });
}

function renderStickers(stickerList) {
  const container = document.getElementById('stickersContainer');
  if (!container) return;
  container.innerHTML = '';

  const positions = [
    { top: '4%', left: '6%', rot: -12 },
    { top: '3%', right: '8%', rot: 15 },
    { top: '50%', left: '3%', rot: -8 },
    { top: '52%', right: '4%', rot: 10 },
    { bottom: '10%', left: '8%', rot: -5 },
    { bottom: '11%', right: '7%', rot: 14 },
    { top: '15%', left: '15%', rot: 6 },
    { top: '18%', right: '16%', rot: -11 }
  ];

  stickerList.forEach((src, idx) => {
    const img = document.createElement('img');
    img.src = src;
    img.className = 'dj-sticker';
    
    const pos = positions[idx % positions.length];
    const rot = pos.rot || (Math.random() * 30 - 15);
    
    if (pos.top) img.style.top = pos.top;
    if (pos.bottom) img.style.bottom = pos.bottom;
    if (pos.left) img.style.left = pos.left;
    if (pos.right) img.style.right = pos.right;

    img.style.transform = `rotate(${rot}deg)`;
    container.appendChild(img);
  });
}

(function() {
  const modal = document.getElementById('legalModal');
  const acceptBtn = document.getElementById('acceptLegalBtn');
  const openTermsBtn = document.getElementById('openTermsBtn');
  const statusMsg = document.getElementById('statusMessage');

  const paypalLink = document.getElementById('paypalLink');
  if (paypalLink) paypalLink.href = 'https://paypal.me/' + PAYPAL_USER_NAME;

  if (localStorage.getItem(STORAGE_PREFIX + 'legalAccepted') === 'true') {
    modal.style.display = 'none';
    if (statusMsg.textContent === 'ACEPTA LOS TÉRMINOS PRIMERO') {
      statusMsg.textContent = 'TOCA PARA INICIAR';
    }
  }

  acceptBtn.addEventListener('click', function(e) {
    e.preventDefault(); e.stopPropagation();
    localStorage.setItem(STORAGE_PREFIX + 'legalAccepted', 'true');
    modal.style.display = 'none';
    statusMsg.textContent = 'TOCA PARA INICIAR';
    if (typeof startRadio === 'function' && tracks && tracks.length > 0) startRadio();
  });

  openTermsBtn.addEventListener('click', function(e) {
    e.preventDefault(); e.stopPropagation();
    modal.style.display = 'flex';
  });

  document.getElementById('linkPrivacy').addEventListener('click', function(e) {
    e.preventDefault();
    alert('Política de Privacidad - LabTeknøRadiø:\n\nNo recopilamos datos personales. Se utiliza almacenamiento local para guardar tu aceptación de términos y pegatinas.');
  });
  document.getElementById('linkTerms').addEventListener('click', function(e) {
    e.preventDefault();
    alert('Términos de Uso - LabTeknøRadiø:\n\nEl contenido musical transmitido pertenece a DaløreX. Queda prohibida la redistribución no autorizada.');
  });
})();

const LOCAL_TRACKS = [
  "track1_liveonthebeat_dalørex.mp3",
  "track2_raveep1_psykodelialabtekno.mp3",
  "track3_fuckwarsep_zair.mp3",
  "track4_accionv1_psykodeliatkno.mp3",
  "track5_velocity_pskodeliateknowaves.mp3",
  "track6_healingfrequencys_psykodeliateknowaves.mp3",
  "track7_Cuoredirave_Valmad.mp3",
  "track8_expaciux_xailor.mp3",
  "track9_raveep1_psykodelialabtekno.mp3",
  "track10_Raveep1_psykodelialabtekno.mp3"
];

const DEMO_TRACK = 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3';

let audioCtx, tracks = [], currentIdx = -1, isPlaying = false, hasStarted = false;
let gainA, gainB, sourceA, sourceB, activeGain = 'A', masterGain, mixTimer, analyser;
let currentMode = 'set';

const MIX_SEGMENT = 144, MIX_CROSSFADE = 15, PLAYLIST_CROSSFADE = 8;
const vizCanvas = document.getElementById('vizCanvas');
const ctxViz = vizCanvas.getContext('2d');
const statusMsg = document.getElementById('statusMessage');
const btnMix = document.getElementById('btnMix');
const btnPlaylist = document.getElementById('btnPlaylist');
let deckA = { source: null, gain: null, startTime: 0, offset: 0 };
let deckB = { source: null, gain: null, startTime: 0, offset: 0 };

function resizeVizCanvas() {
  const rect = vizCanvas.parentElement.getBoundingClientRect();
  vizCanvas.width = rect.width; vizCanvas.height = rect.height;
}
resizeVizCanvas();
window.addEventListener('resize', resizeVizCanvas);

function getAC() {
  if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
  if (audioCtx.state === 'suspended') audioCtx.resume();
  return audioCtx;
}

function setupMaster() {
  const ac = getAC();
  if (!masterGain) {
    masterGain = ac.createGain(); masterGain.gain.value = 0.9;
    analyser = ac.createAnalyser(); analyser.fftSize = 256;
    masterGain.connect(analyser); analyser.connect(ac.destination);
  }
  if (!gainA) { gainA = ac.createGain(); gainA.gain.value = 0; gainA.connect(masterGain); }
  if (!gainB) { gainB = ac.createGain(); gainB.gain.value = 0; gainB.connect(masterGain); }
}

async function loadBufferFromUrl(url) {
  const ac = getAC();
  const resp = await fetch(url);
  if (!resp.ok) throw new Error('HTTP ' + resp.status);
  const buf = await resp.arrayBuffer();
  return await ac.decodeAudioData(buf);
}

async function loadTracks(urlList) {
  for (const url of urlList) {
    try {
      const buffer = await loadBufferFromUrl(url);
      const name = url.split('/').pop().replace(/\.[^/.]+$/, "").toUpperCase();
      tracks.push({ name, url, duration: buffer.duration, buffer });
    } catch (e) {
      console.warn('❌ Falló pista: ' + url);
    }
  }
}

async function initTracks() {
  try {
    statusMsg.textContent = 'CARGANDO LAB-TRACKS...';
    await loadTracks(LOCAL_TRACKS);
    if (tracks.length === 0) {
      statusMsg.textContent = 'MODO DEMO ONLINE...';
      await loadTracks([DEMO_TRACK]);
    }
    if (tracks.length === 0) {
      statusMsg.textContent = 'ERROR: SIN AUDIO';
    } else {
      statusMsg.textContent = (localStorage.getItem(STORAGE_PREFIX + 'legalAccepted') === 'true') 
        ? 'TOCA PARA INICIAR' 
        : 'ACEPTA LOS TÉRMINOS PRIMERO';
      if (hasStarted && tracks.length > 0) startRadio();
    }
  } catch (e) {
    statusMsg.textContent = 'ERROR DE SISTEMA';
  }
}

function stopSource(src) {
  if (src) { try { src.stop(); } catch(e){} src.disconnect(); }
}

function stopAll() {
  stopSource(sourceA); sourceA = null;
  stopSource(sourceB); sourceB = null;
  if (mixTimer) clearTimeout(mixTimer);
}

function transitionToNext() {
  if (!isPlaying || tracks.length === 0) return;
  const nextIdx = (currentIdx + 1) % tracks.length;
  const otherGain = activeGain === 'A' ? gainB : gainA;
  const currentGain = activeGain === 'A' ? gainA : gainB;
  stopSource(activeGain === 'A' ? sourceB : sourceA);
  const source = playSegment(otherGain, nextIdx, 0, 0.001);
  if (source) {
    if (activeGain === 'A') { sourceB = source; activeGain = 'B'; deckB = { source, gain: gainB, startTime: audioCtx.currentTime, offset: 0 }; }
    else { sourceA = source; activeGain = 'A'; deckA = { source, gain: gainA, startTime: audioCtx.currentTime, offset: 0 }; }
    currentIdx = nextIdx;
    const dur = (currentMode === 'mix') ? MIX_CROSSFADE : PLAYLIST_CROSSFADE;
    crossfadeVolumes(currentGain, otherGain, dur);
    scheduleNext();
    statusMsg.textContent = tracks[currentIdx].name;
  }
}

function playSegment(gainNode, trackIndex, startOffset, initialVol) {
  const ac = getAC(); setupMaster();
  if (trackIndex < 0 || trackIndex >= tracks.length) return null;
  const track = tracks[trackIndex];
  const source = ac.createBufferSource();
  source.buffer = track.buffer; source.connect(gainNode);
  const now = ac.currentTime;
  source.start(0, startOffset);
  gainNode.gain.cancelScheduledValues(now);
  gainNode.gain.setValueAtTime(initialVol, now);
  source.onended = () => {
    if (isPlaying && currentIdx === trackIndex) {
      if (mixTimer) clearTimeout(mixTimer);
      transitionToNext();
    }
  };
  if (currentMode === 'mix') {
    const playDur = Math.min(MIX_SEGMENT, track.duration - startOffset);
    source.stop(now + playDur);
    const wait = Math.max(0, playDur - MIX_CROSSFADE);
    mixTimer = setTimeout(() => { if (isPlaying && currentMode === 'mix') transitionToNext(); }, wait * 1000);
  }
  return source;
}

function crossfadeVolumes(fromGain, toGain, duration) {
  const ac = getAC(); const now = ac.currentTime;
  fromGain.gain.cancelScheduledValues(now);
  fromGain.gain.setValueAtTime(fromGain.gain.value || 0.9, now);
  fromGain.gain.linearRampToValueAtTime(0.001, now + duration);
  toGain.gain.cancelScheduledValues(now);
  toGain.gain.setValueAtTime(0.001, now);
  toGain.gain.linearRampToValueAtTime(0.9, now + duration);
}

function scheduleNext() {
  if (!isPlaying || tracks.length === 0) return;
  clearTimeout(mixTimer);
  const deck = (activeGain === 'A') ? deckA : deckB;
  const track = tracks[currentIdx];
  if (!track || !deck.source) { setTimeout(() => { if(isPlaying) transitionToNext(); }, 500); return; }
  const elapsed = audioCtx.currentTime - deck.startTime + deck.offset;
  let remaining = (currentMode === 'mix') ? MIX_SEGMENT - elapsed : track.duration - elapsed;
  const fade = (currentMode === 'mix') ? MIX_CROSSFADE : PLAYLIST_CROSSFADE;
  if (remaining <= fade + 0.5) {
    setTimeout(() => { if(isPlaying) transitionToNext(); }, 100); return;
  }
  mixTimer = setTimeout(() => { if(isPlaying) transitionToNext(); }, (remaining - fade) * 1000);
}

function startRadio() {
  if (tracks.length === 0) return;
  getAC(); setupMaster(); stopAll();
  if (currentIdx < 0 || currentIdx >= tracks.length) currentIdx = 0;
  const source = playSegment(gainA, currentIdx, 0, 0.9);
  if (source) {
    sourceA = source; activeGain = 'A'; deckA = { source, gain: gainA, startTime: audioCtx.currentTime, offset: 0 };
    isPlaying = true; statusMsg.textContent = tracks[currentIdx].name; scheduleNext();
  }
}

function switchMode(mode) {
  if (currentMode === mode || tracks.length === 0) return;
  currentMode = mode;
  btnMix.classList.toggle('active', mode === 'mix');
  btnPlaylist.classList.toggle('active', mode === 'set' || mode === 'playlist');
  if (isPlaying) { stopAll(); startRadio(); }
}

btnMix.addEventListener('click', e => { e.stopPropagation(); switchMode('mix'); });
btnPlaylist.addEventListener('click', e => { e.stopPropagation(); switchMode('set'); });

function handleFirstTouch(e) {
  if (document.getElementById('legalModal').style.display !== 'none') return;
  if (e.target === btnMix || e.target === btnPlaylist || e.target.closest('.bottom-btn') || e.target.closest('.upload-btn-label')) return;
  if (hasStarted) {
    if (e.target.closest('.display-screen') || e.target.id === 'vizCanvas') {
      if (isPlaying) { stopAll(); isPlaying = false; statusMsg.textContent = 'PAUSA'; }
      else startRadio();
    }
    return;
  }
  getAC(); hasStarted = true;
  if (tracks.length === 0) { initTracks().then(() => { if(tracks.length>0) startRadio(); }); }
  else startRadio();
}

document.body.addEventListener('click', handleFirstTouch);
document.body.addEventListener('touchstart', handleFirstTouch);

function drawVisualizer() {
  requestAnimationFrame(drawVisualizer);
  const w = vizCanvas.width, h = vizCanvas.height;
  const cx = w/2, cy = h/2, baseRadius = Math.min(w,h)*0.28, time = Date.now()*0.008;
  ctxViz.clearRect(0,0,w,h);

  if (!analyser || !isPlaying) {
    ctxViz.beginPath(); ctxViz.arc(cx,cy,baseRadius+Math.sin(time*0.8)*4,0,Math.PI*2);
    ctxViz.strokeStyle='hsla(190,100%,50%,0.5)'; ctxViz.lineWidth=2; ctxViz.stroke();
    return;
  }

  const bufferLength = analyser.frequencyBinCount;
  const dataArray = new Uint8Array(bufferLength);
  analyser.getByteFrequencyData(dataArray);
  let avg = 0; for(let i=0;i<bufferLength;i++) avg+=dataArray[i]; avg=avg/bufferLength/255;

  const glow = ctxViz.createRadialGradient(cx,cy,baseRadius*0.4,cx,cy,baseRadius*1.6);
  glow.addColorStop(0,'hsla(210,100%,50%,0.25)'); glow.addColorStop(1,'hsla(190,100%,50%,0)');
  ctxViz.fillStyle=glow; ctxViz.beginPath(); ctxViz.arc(cx,cy,baseRadius*1.6,0,Math.PI*2); ctxViz.fill();

  const mainRadius = baseRadius*(0.85+avg*0.65);
  const mainGrad = ctxViz.createRadialGradient(cx,cy,0,cx,cy,mainRadius);
  mainGrad.addColorStop(0,'hsla(220,100%,60%,0.3)');
  mainGrad.addColorStop(0.7,'hsla(190,100%,50%,0.6)');
  mainGrad.addColorStop(1,'hsla(180,100%,60%,0.9)');
  ctxViz.fillStyle=mainGrad; ctxViz.beginPath(); ctxViz.arc(cx,cy,mainRadius,0,Math.PI*2); ctxViz.fill();

  ctxViz.beginPath(); ctxViz.arc(cx,cy,mainRadius,0,Math.PI*2);
  ctxViz.strokeStyle='hsla(180,100%,75%,0.9)'; ctxViz.lineWidth=2; ctxViz.stroke();

  for(let i=0;i<64;i++) {
    const val = dataArray[Math.floor(i*bufferLength/64)]/255;
    const angle = (i/64)*Math.PI*2-Math.PI/2+time*1.5;
    const spikeLen = val*baseRadius*1.2;
    ctxViz.beginPath();
    ctxViz.moveTo(cx+Math.cos(angle)*mainRadius, cy+Math.sin(angle)*mainRadius);
    ctxViz.lineTo(cx+Math.cos(angle)*(mainRadius+spikeLen), cy+Math.sin(angle)*(mainRadius+spikeLen));
    ctxViz.strokeStyle=`hsla(${180 + (i*2)%40},100%,60%,${0.5+val*0.5})`;
    ctxViz.lineWidth=1.5+val*2; ctxViz.stroke();
  }

  for(let i=0;i<40;i++) {
    const val = dataArray[Math.floor(i*bufferLength/40)]/255;
    const barHeight = val*h*0.4;
    ctxViz.fillStyle=`hsla(${190 + (i*2)},100%,55%,0.65)`;
    ctxViz.fillRect(i*(w/40), h-barHeight, (w/40)-2, barHeight);
  }
}

drawVisualizer();
initStickerSystem();
initTracks();
